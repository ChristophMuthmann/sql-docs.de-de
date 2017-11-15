---
title: "Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten (Always On-Verfügbarkeitsgruppen) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/01/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 2d54e433746548bcef8cb0780f8586ec2568d898
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="active-secondaries-backup-on-secondary-replicas-always-on-availability-groups"></a>Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten (AlwaysOn-Verfügbarkeitsgruppen)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Die Funktionen für aktive sekundäre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Replikate umfassen auch die Unterstützung von Sicherungsvorgängen auf sekundären Replikaten. Sicherungsvorgänge können E/A und CPU (mit Sicherungskomprimierung) erheblich belasten. Durch die Auslagerung von Sicherungen auf ein sekundäres Replikat mit dem Status SYNCHRONIZED oder SYNCHRONIZING können Sie die Ressourcen auf der Serverinstanz verwenden, die das primäre Replikat für Arbeitsauslastungen erster Ebene hostet.  

> [!NOTE]  
>  RESTORE-Anweisungen sind in den primären und sekundären Datenbanken einer Verfügbarkeitsgruppe nicht zulässig.  
  
-   [Unterstützte Sicherungstypen](#SupportedBuTypes)  
  
-   [Konfigurieren, wo Sicherungsaufträge ausgeführt werden](#WhereBuJobsRun)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="SupportedBuTypes"></a> Auf sekundären Replikaten unterstützte Sicherungstypen  
  
-   **BACKUP DATABASE** unterstützt vollständige Kopiesicherungen von Datenbanken, Dateien oder Dateigruppen nur bei der Ausführung auf sekundären Replikaten. Beachten Sie, dass sich Kopiesicherungen nicht auf die Protokollkette auswirken bzw. kein differenzielles Bitmuster löschen.  
  
-   Differenzielle Sicherungen werden auf sekundären Replikaten nicht unterstützt.  
  
-   **BACKUP LOG** unterstützt nur reguläre Protokollsicherungen (die COPY_ONLY-Option wird für Protokollsicherungen auf sekundären Replikaten nicht unterstützt).  
  
     Bei sämtlichen Protokollsicherungen von Replikaten (primär oder sekundär) wird ungeachtet ihres Verfügbarkeitsmodus (mit synchronem Commit oder mit asynchronem Commit) eine konsistente Protokollkette sichergestellt.  
  
-   Zum Sichern einer sekundären Datenbank muss ein sekundäres Replikat mit dem primären Replikat kommunizieren können und den Status **SYNCHRONIZED** oder **SYNCHRONIZING**aufweisen.  

In einer verteilten Verfügbarkeitsgruppe können Sicherungen auf dem sekundären Replikat durchgeführt werden, das sich in derselben Verfügbarkeitsgruppe wie das primäre Replikat befindet oder auf dem primären Replikat jeder sekundären Verfügbarkeitsgruppe. Sicherungen können nicht auf einem sekundären Replikat in einer sekundären Verfügbarkeitsgruppe durchgeführt werden, da sekundäre Replikate nur mit dem primären Replikat ihrer eigenen Verfügbarkeitsgruppe kommunizieren. Nur für Replikate, die direkt mit dem globalen primären Replikat kommunizieren, können Sicherungsvorgänge durchgeführt werden.

##  <a name="WhereBuJobsRun"></a> Konfigurieren, wo Sicherungsaufträge ausgeführt werden  
 Das Ausführen von Sicherungen auf einem sekundären Replikat zum Auslagern der Sicherungsarbeitsauslastung vom primären Produktionsserver ist ein großer Vorteil. Durch die Ausführung von Sicherungen auf sekundären Replikaten wird es jedoch wesentlich komplexer, den Ausführungsort von Sicherungsaufträgen zu bestimmen. Um diesen Vorgang zu vereinfachen, konfigurieren Sie den Ausführungsort von Sicherungsaufträgen wie folgt:  
  
1.  Konfigurieren Sie die Verfügbarkeitsgruppe, um anzugeben, welche Verfügbarkeitsreplikate am Ort, an dem Sie Sicherungen wünschen, ausgeführt werden sollen. Weitere Informationen finden Sie unter den Parametern *AUTOMATED_BACKUP_PREFERENCE* und *BACKUP_PRIORITY* in [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) oder [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)aufweisen.  
  
2.  Erstellen Sie skriptbasierte Sicherungsaufträge für jede Verfügbarkeitsdatenbank auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat hostet, das für das Ausführen von Sicherungen infrage kommt. Weitere Informationen finden Sie im Abschnitt „Nachverfolgung: Nach dem Konfigurieren einer Sicherung auf sekundären Replikaten“ von [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)aufweisen.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie die Sicherung auf sekundären Replikaten**  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 **So bestimmen Sie, ob es sich beim aktuellen Replikat um ein bevorzugtes Sicherungsreplikat handelt**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **So erstellen Sie einen Sicherungsauftrag**  
  
-   [Verwenden des Wartungsplanungs-Assistenten](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [Implementieren von Aufträgen](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Kopiesicherungen &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
