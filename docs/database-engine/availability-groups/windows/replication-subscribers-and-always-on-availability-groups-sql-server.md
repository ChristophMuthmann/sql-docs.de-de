---
title: "Replikationsabonnenten und Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e868d03cfe57b78affa81b00f5f91376ae9a89e8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="replication-subscribers-and-always-on-availability-groups-sql-server"></a>Replikationsabonnenten und Always On-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Wenn für eine Always On-Verfügbarkeitsgruppe mit einer Datenbank, die einen Replikationsabonnenten darstellt, ein Failover ausgeführt wird, tritt u.U. ein Fehler beim Replikationsabonnement auf. Bei Transaktionsabonnenten setzt der Verteilungs-Agent die Replikation automatisch fort, wenn für das Abonnement der Name des Verfügbarkeitsgruppenlisteners des Abonnenten verwendet wird. Bei Mergeabonnenten muss der Abonnent vom Replikationsadministrator manuell neu konfiguriert werden, indem er das Abonnement neu erstellt.  
  
## <a name="what-is-supported"></a>Unterstützte Vorgänge  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikation unterstützt das automatische Failover des Verlegers, das automatische Failover von Transaktionsabonnenten und das manuelle Failover von Mergeabonnenten. Das Failover eines Verteilers zu einer Verfügbarkeitsdatenbank wird nicht unterstützt. Always On kann nicht mit WebSync- und ssNoVersion Compact-Szenarien kombiniert werden.  
  
 **Failover eines Mergepullabonnements**  
  
 Ein Pullabonnement schlägt bei einem Verfügbarkeitsgruppenfailover fehl, da der Pull-Agent die Aufträge nicht finden kann, die in der **msdb** -Datenbank der Serverinstanz gespeichert sind, von der das primäre Replikat gehostet wird. Die Datenbank ist nicht verfügbar, da ein Serverinstanzfehler aufgetreten ist.  
  
 **Failover eines Mergepushabonnements**  
  
 Ein Pushabonnement schlägt bei einem Verfügbarkeitsgruppenfailover fehl, da der Push-Agent keine Verbindung mehr mit der ursprünglichen Abonnementdatenbank auf dem ursprünglichen Abonnenten herstellen kann.  
  
## <a name="how-to-create-transactional-subscription-in-an-always-on-environment"></a>Erstellen eines Transaktionsabonnements in einer Always On-Umgebung  
 Führen Sie bei der Transaktionsreplikation folgende Schritte aus, um die Verfügbarkeitsgruppe eines Abonnenten zu konfigurieren und ein Failover auszuführen:  
  
1.  Bevor Sie das Abonnement erstellen, fügen Sie der entsprechenden Always On-Verfügbarkeitsgruppe die Abonnentendatenbank hinzu.  
  
2.  Fügen Sie den Verfügbarkeitsgruppenlistener des Abonnenten allen Knoten der Verfügbarkeitsgruppe als Verbindungsserver hinzu. Dadurch werden alle potenziellen Failoverpartner informiert, dass der Listener vorhanden und für Verbindungen verfügbar ist.  
  
3.  Erstellen Sie das Abonnement mit dem Namen des Verfügbarkeitsgruppenlisteners des Abonnenten mithilfe des Skripts im Abschnitt **Erstellen eines Pushabonnements für eine Transaktionsreplikation** unten. Der Listenername bleibt nach einem Failover weiterhin gültig, während der tatsächliche Servername des Abonnenten von dem Knoten abhängig ist, der zum neuen primären Replikat wird.  
  
    > [!NOTE]  
    >  Das Abonnement muss mithilfe eines [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skripts erstellt werden, nicht mit [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
4.  Bei Erstellung eines Pullabonnements:  
  
    1.  Öffnen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]auf dem primären Abonnentenknoten die Struktur des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agents.  
  
    2.  Suchen Sie den **Agentauftrag zur Verteilung des Pullabonnements**, und bearbeiten Sie den Auftrag.  
  
    3.  Überprüfen Sie im Schritt zum **Ausführen des Agentauftrags** den `-Publisher` -Parameter und den `-Distributor` -Parameter. Stellen Sie sicher, dass diese Parameter den richtigen direkten Server- und Instanznamen des Verleger- und Verteilerservers enthalten.  
  
    4.  Ändern Sie den `-Subscriber` -Parameter in den Verfügbarkeitsgruppenlistener-Namen des Abonnenten.  
  
 Wenn Sie beim Erstellen des Abonnements diese Schritte befolgen, müssen nach einem Failover keine weiteren Maßnahmen ergriffen werden.  
  
## <a name="creating-a-transactional-replication-push-subscription"></a>Erstellen eines Pushabonnements für eine Transaktionsreplikation  
  
```  
-- commands to execute at the publisher, in the publisher database:  
use [<publisher database name>]  
EXEC sp_addsubscription @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @destination_db = N'<subscriber database name>',   
       @subscription_type = N'Push',   
       @sync_type = N'automatic', @article = N'all', @update_mode = N'read only', @subscriber_type = 0;  
GO  
  
EXEC sp_addpushsubscription_agent @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @subscriber_db = N'<subscriber database name>',   
       @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO  
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>So setzen Sie Merge-Agents nach einem Verfügbarkeitsgruppenfailover des Abonnenten fort  
 Bei einer Mergereplikation muss der Abonnent mithilfe folgender Schritte von einem Replikationsadministrator manuell neu konfiguriert werden:  
  
1.  Führen Sie **sp_subscription_cleanup** aus, um das alte Abonnement für den Abonnenten zu entfernen. Führen Sie diese Aktion für das neue primäre Replikat aus (das zuvor das sekundäre Replikat war).  
  
2.  Erstellen Sie das Abonnement neu, indem Sie ein neues Abonnement auf Grundlage einer neuen Momentaufnahme erstellen.  
  
> [!NOTE]  
>  Das aktuelle Verfahren ist für Mergereplikationsabonnenten nicht geeignet, die Mergereplikation erfolgt jedoch hauptsächlich für nicht verbundene Benutzer (Desktops, Laptops, Mobiltelefone), die keine Always On-Verfügbarkeitsgruppen auf dem Abonnenten nutzen.  
  
  
