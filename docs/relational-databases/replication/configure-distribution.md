---
title: Konfigurieren der Verteilung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2aa81e571c53a0271b1c795198f206735abb3f32
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-distribution"></a>Konfigurieren der Verteilung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Bei dem Verteiler handelt es sich um einen Server, der die Verteilungsdatenbank enthält. In der Datenbank sind Metadaten und Verlaufsdaten für alle Replikations- und Transaktionstypen der Transaktionsreplikation gespeichert. Zum Einrichten der Replikation müssen Sie einen Verteiler konfigurieren. Jeder Verleger kann nur einer einzigen Verteilerinstanz zugewiesen werden, es kann jedoch für mehrere ein Verteiler freigegeben werden. Der Verteiler verwendet die folgenden zusätzlichen Ressourcen auf dem Server, auf dem er sich befindet:  
  
-   Zusätzlichen Speicherplatz, falls die Momentaufnahmedateien für die Veröffentlichung auf dem Verteiler gespeichert werden (was in der Regel der Fall ist).  
  
-   Zusätzlichen Speicherplatz zum Speichern der Verteilungsdatenbank.  
  
-   Zusätzliche Prozessornutzung durch Replikations-Agents für auf dem Verteiler ausgeführte Pushabonnements.  
  
 Der Server, den Sie als Verteiler auswählen, sollte ausreichend Speicherplatz und Prozessorleistung für die Replikation und sonstige Aktivitäten, die auf diesem Server basieren, aufweisen. Beim Konfigurieren des Verteilers geben Sie Folgendes an:  
  
-   Einen Momentaufnahmeordner, der standardmäßig für alle Verleger verwendet wird, die diesen Verteiler verwenden. Stellen Sie sicher, dass dieser Ordner bereits freigegeben ist und die richtigen Berechtigungen festgelegt sind. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
-   Einen Namen und Dateispeicherorte für die Verteilungsdatenbank. Die Verteilungsdatenbank kann nach dem Erstellen nicht mehr umbenannt werden. Wenn Sie einen anderen Namen für die Datenbank verwenden möchten, müssen Sie die Verteilung deaktivieren und neu konfigurieren.  
  
-   Alle Verleger, die den Verteiler verwenden dürfen. Wenn Sie andere Verleger angeben als die Instanz, auf der der Verteiler ausgeführt wird, müssen Sie auch ein Kennwort für die Verbindungen angeben, die die Verleger mit dem Remoteverteiler herstellen.  
  
 Führen Sie bei der Transaktionsreplikation nach dem Konfigurieren der Verteilung folgende Aktionen aus:  
  
-   Richten Sie eine angemessene Größe für die Verteilungsdatenbank ein. Testen Sie die Replikation unter der typischen Auslastung des Systems, um den Speicherbedarf für Befehle zu ermitteln. Stellen Sie sicher, dass die Datenbank ausreichend Speicherkapazität für Befehle aufweist, um die häufige automatische Vergrößerung zu verhindern. Weitere Informationen zum Ändern der Größe einer Datenbank finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Legen Sie die Option **sync with backup** für die Verteilungsdatenbank fest. Weitere Informationen finden Sie unter [Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md) und [Aktivieren koordinierter Sicherungen für die Transaktionsreplikation &#40;Replication Transact-SQL Programming&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).  
  
## <a name="local-and-remote-distributors"></a>Lokale und Remoteverteiler  
 Standardmäßig handelt es sich beim Verteiler um den gleichen Server wie beim Verleger (ein lokaler Verteiler), der Verteiler kann jedoch auch ein anderer Server sein als der Verleger (ein Remoteverteiler). In der Regel verwenden Sie in den folgenden Fällen einen Remoteverteiler:  
  
-   Zum Auslagern der Verarbeitung auf einen anderen Computer, wenn sich die Replikation so wenig wie möglich auf den Verleger auswirken soll (z. B. wenn der Verleger ein OLTP-Server ist).  
  
-   Zum Konfigurieren eines zentralen Verteilers für mehrere Verleger.  
  
 Remoteverteiler treten bei der Transaktionsreplikation häufiger auf als bei der Mergereplikation. Dafür gibt es zwei Gründe:  
  
-   Der Verteiler spielt bei der Transaktionsreplikation eine größere Rolle, da alle replizierten Transaktionen in die Verteilungsdatenbank geschrieben werden oder daraus gelesen werden.  
  
-   Mergereplikationstoplogien verwenden im Allgemeinen Pullabonnements. Deshalb werden Agents jeweils auf einzelnen Abonnenten und nicht alle auf dem Verteiler ausgeführt. Weitere Informationen finden Sie unter [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md). In den meisten Fällen sollten Sie einen lokalen Verteiler für die Mergereplikation verwenden.  
  
 Informationen zum Konfigurieren Sie der Veröffentlichung und Verteilung finden Sie unter [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
 Informationen zum Ändern der Verleger- und Verteilereigenschaften finden Sie unter [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Schützen des Verteilers](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
