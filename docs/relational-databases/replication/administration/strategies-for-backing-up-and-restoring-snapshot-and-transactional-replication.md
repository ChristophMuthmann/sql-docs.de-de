---
title: Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation | Microsoft Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backups [SQL Server replication], snapshot replication
- restoring [SQL Server replication], transactional replication
- snapshot replication [SQL Server], backup and restore
- restoring [SQL Server replication], snapshot replication
- recovery [SQL Server replication], transactional replication
- transactional replication, backup and restore
- recovery [SQL Server replication], snapshot replication
- sync with backup [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 58cc3e019838c102405191b25ef734b011915244
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication"></a>Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation
  Drei Bereiche sind beim Entwickeln einer Sicherungs- und Wiederherstellungsstrategie für die Momentaufnahme- und Transaktionsreplikation zu berücksichtigen:  
  
-   Die zu sichernden Datenbanken.  
  
-   Die Sicherungseinstellungen für die Transaktionsreplikation.  
  
-   Die zum Wiederherstellen einer Datenbank erforderlichen Schritte. Diese hängen vom Typ der Replikation und den Optionen ab, der bzw. die ausgewählt werden.  
  
 In diesem Thema wird jeder dieser Bereiche in den nächsten drei Abschnitten erläutert. Weitere Informationen zum Sichern und Wiederherstellen bei Oracle-Verlegern finden Sie unter [Sichern und Wiederherstellen bei Oracle-Verlegern](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md).  
  
## <a name="backing-up-databases"></a>Sichern von Datenbanken  
 Sichern Sie bei der Momentaufnahme- und Transaktionsreplikation regelmäßig die folgenden Datenbanken:  
  
-   Veröffentlichungsdatenbank auf dem Verleger  
  
-   Verteilungsdatenbank auf dem Verteiler  
  
-   Abonnementdatenbank auf den einzelnen Abonnenten  
  
-   Die Systemdatenbanken **master** und **msdb** auf dem Verleger, Verteiler und allen Abonnenten. Diese Datenbanken sollten zur selben Zeit wie alle anderen Datenbanken und die entsprechende Replikationsdatenbank gesichert werden. Sichern Sie also z. B. die **master** -Datenbank und die **msdb** -Datenbank auf dem Verleger immer dann, wenn Sie auch die Veröffentlichungsdatenbank sichern. Wenn die Veröffentlichungsdatenbank wiederhergestellt wird, stellen Sie sicher, dass die **master** -Datenbank und die **msdb** -Datenbank hinsichtlich der Replikationskonfiguration und -einstellungen mit der Veröffentlichungsdatenbank konsistent sind.  
  
 Wenn Sie regelmäßige Protokollsicherungen ausführen, sollten in den Protokollsicherungen auch alle replikationsrelevanten Änderungen erfasst werden. Wenn Sie keine Protokollsicherungen ausführen, sollte immer dann eine Sicherungskopie erstellt werden, wenn eine für die Replikation relevante Einstellung geändert wird. Weitere Informationen finden Sie unter [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-settings-for-transactional-replication"></a>Sicherungseinstellungen für die Transaktionsreplikation  
 Die Transaktionsreplikation schließt die Verwendung der Option **sync with backup** ein, die für die Verteilungsdatenbank und die Veröffentlichungsdatenbank festgelegt werden kann:  
  
-   Es wird empfohlen, diese Option für die Verteilungsdatenbank immer festzulegen.  
  
     Mit dieser Option wird sichergestellt, dass Transaktionen im Protokoll der Veröffentlichungen nicht abgeschnitten werden, bevor sie in der Verteilungsdatenbank gesichert wurden. Die Verteilungsdatenbank kann auf die letzte Sicherung wiederhergestellt werden. Eventuell fehlende Transaktionen werden von der Veröffentlichungsdatenbank an die Verteilungsdatenbank übermittelt. Die Replikation wird ohne Einschränkungen fortgesetzt.  
  
     Das Festlegen dieser Option für die Verteilungsdatenbank wirkt sich nicht auf die Replikationslatenzzeit aus. Mit dem Festlegen dieser Option wird die Kürzung des Protokolls der Veröffentlichungsdatenbank so lange verzögert, bis die entsprechenden Transaktionen in der Verteilungsdatenbank gesichert sind. (Dies kann zur Erstellung eines umfangreicheren Transaktionsprotokolls in der Veröffentlichungsdatenbank führen.)  
  
-   Es wird empfohlen, diese Option für die Veröffentlichungsdatenbank festzulegen, falls die Anwendung eine zusätzliche Latenzzeit unterstützt.  
  
     Wenn Sie diese Option für die Veröffentlichungsdatenbank festlegen, stellen Sie sicher, dass Transaktionen erst an die Verteilungsdatenbank übermittelt werden, wenn Sie in der Veröffentlichungsdatenbank gesichert wurden. Die letzte Sicherung der Veröffentlichungsdatenbank kann dann auf dem Verleger wiederhergestellt werden, und es besteht keine Möglichkeit, dass die Verteilungsdatenbank Transaktionen enthält, die in der wiederhergestellten Veröffentlichungsdatenbank nicht vorhanden sind.  
  
     Latenzzeit und Durchsatz sind betroffen, da Transaktionen erst an die Verteilungsdatenbank übermittelt werden können, nachdem sie auf dem Verleger gesichert wurden. Wenn z. B. das Transaktionsprotokoll alle fünf Minuten gesichert wird, entsteht eine zusätzliche Latenzzeit von fünf Minuten zwischen dem Ausführen des Commit für eine Transaktion auf dem Verleger und dem Übermitteln der Transaktion an die Verteilungsdatenbank und anschließend an den Abonnenten.  
  
    > [!NOTE]  
    >  Mit der Option **sync with backup** wird die Konsistenz zwischen der Veröffentlichungsdatenbank und der Verteilungsdatenbank sichergestellt, sie ist jedoch kein Garant gegen Datenverlust. Wenn z. B. das Transaktionsprotokoll verloren geht, sind Transaktionen, für die seit der letzten Sicherung des Transaktionsprotokolls ein Commit ausgeführt wurde, nicht in der Veröffentlichungsdatenbank oder der Verteilungsdatenbank verfügbar. Das ist das gleiche Verhalten wie bei einer nicht replizierten Datenbank.  
  
 **So legen Sie die Option sync with backup fest**  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] Replikationsprogrammierung: [Aktivieren Sie koordinierte Sicherungen für die Transaktionsreplikation &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
## <a name="restoring-databases-involved-in-replication"></a>Wiederherstellen der an der Replikation beteiligten Datenbanken  
 Wenn aktuelle Sicherungen verfügbar sind und die entsprechenden Schritte befolgt werden, können Sie alle Datenbanken einer Replikationstopologie wiederherstellen. Die Wiederherstellungsschritte für die Veröffentlichungsdatenbank hängen vom Typ der verwendeten Replikation und den verwendeten Optionen ab. Die Wiederherstellungsschritte für alle anderen Datenbanken sind jedoch vom Typ und den Optionen unabhängig.  
  
 Die Replikation ermöglicht das Wiederherstellen replizierter Datenbanken auf dem Server und in die Datenbank, die zum Erstellen der Sicherung herangezogen wurden. Wenn Sie eine Sicherungskopie einer replizierten Datenbank auf einem anderen Server bzw. in einer anderen Datenbank wiederherstellen, können Replikationseinstellungen nicht beibehalten werden. In diesem Fall müssen nach der Wiederherstellung der Sicherungskopien sämtliche Veröffentlichungen und Abonnements neu erstellt werden.  
  
### <a name="publisher"></a>Verleger  
 Wiederherstellungsschritte werden für die folgenden Replikationstypen bereitgestellt:  
  
-   Momentaufnahmereplikation  
  
-   Schreibgeschützte Transaktionsreplikation  
  
-   Transaktionsreplikation mit Updateabonnements  
  
-   Peer-zu-Peer-Transaktionsreplikation  
  
 Die Wiederherstellung der Datenbanken **msdb** und **master** (ebenfalls in diesem Abschnitt erläutert) verläuft bei allen vier Typen gleich.  
  
#### <a name="publication-database-snapshot-replication"></a>Veröffentlichungsdatenbank: Momentaufnahmereplikation  
  
1.  Stellen Sie die aktuellste Sicherung der Veröffentlichungsdatenbank wieder her. Fahren Sie mit Schritt 2 fort.  
  
2.  Enthält die Sicherung der Veröffentlichungsdatenbank die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zum Entfernen einer Replikation finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
#### <a name="publication-database-read-only-transactional-replication"></a>Veröffentlichungsdatenbank: Schreibgeschützte Transaktionsreplikation  
  
1.  Stellen Sie die aktuellste Sicherung der Veröffentlichungsdatenbank wieder her. Fahren Sie mit Schritt 2 fort.  
  
2.  War die Einstellung **sync with backup** vor dem Fehler für die Veröffentlichungsdatenbank aktiviert? Wenn ja, fahren Sie mit Schritt 3 fort, wenn nein, fahren Sie mit Schritt 5 fort.  
  
     Wenn die Einstellung aktiviert ist, gibt die Abfrage `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` den Wert 1 zurück.  
  
3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 4 fort.  
  
4.  Die Konfigurationsinformationen in der wiederhergestellten Veröffentlichungsdatenbank sind nicht aktuell. Deshalb müssen Sie sicherstellen, dass die Abonnenten alle ausstehenden Befehle in der Verteilungsdatenbank aufweisen. Löschen Sie anschließend die Replikationskonfiguration, und erstellen Sie sie erneut.  
  
    1.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Überprüfen Sie, ob alle Befehle an die Abonnenten übermittelt wurden. Verwenden Sie dazu im Replikationsmonitor die Registerkarte **Nicht verteilte Befehle** , oder fragen Sie die [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) -Sicht in der Verteilungsdatenbank ab. Fahren Sie mit Schritt b fort.  
  
         Weitere Informationen zum Starten und Beenden eines Verteilungs-Agents finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Weitere Informationen zum Überprüfen von Befehlen finden Sie unter [Anzeigen von replizierten Befehlen und anderen Informationen in der Verteilungsdatenbank &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) und [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
    2.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zum Entfernen einer Replikation finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen zum Angeben, dass der Abonnement bereits über die Daten verfügt, finden Sie unter [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
5.  Die Option **sync with backup** wurde nicht für die Veröffentlichungsdatenbank festgelegt. Deshalb wurden Transaktionen, die nicht in die wiederhergestellte Sicherung eingeschlossen waren, möglicherweise an den Verteiler und die Abonnenten übermittelt. Stellen Sie nun sicher, dass die Abonnenten über alle ausstehenden Befehle in der Verteilungsdatenbank verfügen. Wenden Sie dann manuell alle Transaktionen auf die Veröffentlichungsdatenbank an, die nicht in die wiederhergestellte Sicherung eingeschlossen waren.  
  
    > [!IMPORTANT]  
    >  Beim Ausführen dieses Prozesses kann es passieren, dass veröffentlichte Tabellen auf einen Stand wiederhergestellt werden, der vor dem Stand anderer nicht veröffentlichter Tabellen liegt, die aus der Sicherung wiederhergestellt werden.  
  
    1.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Überprüfen Sie, ob alle Befehle an die Abonnenten übermittelt wurden. Verwenden Sie dazu im Replikationsmonitor die Registerkarte **Nicht verteilte Befehle** , oder fragen Sie die [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) -Sicht in der Verteilungsdatenbank ab. Fahren Sie mit Schritt b fort.  
  
         Weitere Informationen zum Starten und Beenden eines Verteilungs-Agents finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Weitere Informationen zum Überprüfen von Befehlen finden Sie unter [Anzeigen von replizierten Befehlen und anderen Informationen in der Verteilungsdatenbank &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) und [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
    2.  Verwenden Sie das [Hilfsprogramm "tablediff"](../../../tools/tablediff-utility.md) oder ein anderes Tool, um den Verleger manuell mit dem Abonnenten zu synchronisieren. So können Sie Daten aus der Abonnementdatenbank wiederherstellen, die nicht in der Sicherung der Veröffentlichungsdatenbank enthalten waren. Fahren Sie mit Schritt c fort.  
  
         Weitere Informationen zu den **Tablediff**-Dienstprogramm finden Sie unter [Überprüfen replizierter Tabellen auf Unterschiede &#40;Replikationsprogrammierung&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, führen Sie die gespeicherte Prozedur [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) aus, um die Metadaten des Verlegers erneut mit denen des Verteilers zu synchronisieren. Die Wiederherstellung ist abgeschlossen. Wenn nein, fahren Sie mit Schritt d fort.  
  
    4.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zum Entfernen einer Replikation finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen zum Angeben, dass der Abonnement bereits über die Daten verfügt, finden Sie unter [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### <a name="publication-database-transactional-replication-with-updating-subscriptions"></a>Veröffentlichungsdatenbank: Transaktionsreplikation mit Updateabonnements  
  
1.  Stellen Sie die aktuellste Sicherung der Veröffentlichungsdatenbank wieder her. Fahren Sie mit Schritt 2 fort.  
  
2.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Überprüfen Sie, ob alle Befehle an die Abonnenten übermittelt wurden. Verwenden Sie dazu im Replikationsmonitor die Registerkarte **Nicht verteilte Befehle** , oder fragen Sie die [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) -Sicht in der Verteilungsdatenbank ab. Fahren Sie mit Schritt 3 fort.  
  
     Weitere Informationen zum Starten und Beenden eines Verteilungs-Agents finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
     Weitere Informationen zum Überprüfen von Befehlen finden Sie unter [Anzeigen von replizierten Befehlen und anderen Informationen in der Verteilungsdatenbank &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) und [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
3.  Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden, stellen Sie mit jedem Abonnenten eine Verbindung her, und löschen Sie in der Abonnementdatenbank alle Zeilen aus der [MSreplication_queue &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md)-Tabelle. Fahren Sie mit Schritt 4 fort.  
  
    > [!NOTE]  
    >  Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden und Tabellen Identitätsspalten enthalten, müssen Sie sicherstellen, dass nach jeder Wiederherstellung die richtigen Identitätsbereiche zugewiesen werden. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
4.  Stellen Sie nun sicher, dass die Abonnenten über alle ausstehenden Befehle in der Verteilungsdatenbank verfügen. Wenden Sie dann manuell alle Transaktionen auf die Veröffentlichungsdatenbank an, die nicht in die wiederhergestellte Sicherung eingeschlossen waren.  
  
    > [!IMPORTANT]  
    >  Beim Ausführen dieses Prozesses kann es passieren, dass veröffentlichte Tabellen auf einen Stand wiederhergestellt werden, der vor dem Stand anderer nicht veröffentlichter Tabellen liegt, die aus der Sicherung wiederhergestellt werden.  
  
    1.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Überprüfen Sie, ob alle Befehle an den Abonnenten übermittelt wurden. Verwenden Sie dazu den Replikationsmonitor, oder fragen Sie die [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) -Sicht in der Verteilungsdatenbank ab. Fahren Sie mit Schritt b fort.  
  
    2.  Verwenden Sie das [tablediff Utility](../../../tools/tablediff-utility.md) oder ein anderes Tool, um den Verleger manuell mit dem Abonnenten zu synchronisieren. So können Sie Daten aus der Abonnementdatenbank wiederherstellen, die nicht in der Sicherung der Veröffentlichungsdatenbank enthalten waren. Fahren Sie mit Schritt c fort.  
  
         Weitere Informationen zu den **tablediff**-Dienstprogramm finden Sie unter [Überprüfen replizierter Tabellen auf Unterschiede &#40;Replikationsprogrammierung&#41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, führen Sie die gespeicherte Prozedur [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) aus, um die Metadaten des Verlegers erneut mit denen des Verteilers zu synchronisieren. Die Wiederherstellung ist abgeschlossen. Wenn nein, fahren Sie mit Schritt d fort.  
  
    4.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zum Entfernen einer Replikation finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen zum Angeben, dass der Abonnement bereits über die Daten verfügt, finden Sie unter [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### <a name="publication-database-peer-to-peer-transactional-replication"></a>Veröffentlichungsdatenbank: Peer-zu-Peer-Transaktionsreplikation  
 In den folgenden Schritten sind die Veröffentlichungsdatenbanken **A**, **B**und **C** Bestandteil einer Peer-zu-Peer-Transaktionsreplikationstopologie. Die Datenbanken **A** und **C** sind online und funktionieren ordnungsgemäß; Datenbank **B** muss wiederhergestellt werden. Der hier beschriebene Prozess, insbesondere die Schritte 7, 10 und 11, ist vergleichbar mit dem Prozess zum Hinzufügen eines Knotens zu einer Peer-zu-Peer-Topologie. Die einfachste Möglichkeit zum Ausführen dieser Schritte ist diejenige mithilfe des Assistenten zum Konfigurieren der Peer-zu-Peer-Topologie. Sie können jedoch auch gespeicherte Prozeduren dafür verwenden.  
  
1.  Führen Sie die Verteilungs-Agents aus, um die Abonnements in den Datenbanken **A** und **C** zu synchronisieren. Fahren Sie mit Schritt 2 fort.  
  
     Weitere Informationen zum Starten und Beenden eines Verteilungs-Agents finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Wenn die von **B** verwendete Verteilungsdatenbank noch verfügbar ist, führen Sie die Verteilungs-Agents zum Synchronisieren der Abonnements zwischen den Datenbanken **B** und **A** und den Datenbanken B und **C** aus. Fahren Sie mit Schritt 3 fort.  
  
3.  Entfernen Sie Metadaten aus der von **B** verwendeten Verteilungsdatenbank. Führen Sie dazu in der Verteilungsdatenbank [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md) für **B** aus. Fahren Sie mit Schritt 4 fort.  
  
4.  Löschen Sie in den Datenbanken **A** und **C** die Abonnements für die Veröffentlichung in Datenbank **B**. Fahren Sie mit Schritt 5 fort.  
  
     Weitere Informationen zum Löschen von Abonnements finden Sie unter [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
5.  Führen Sie eine Protokollsicherung oder eine vollständige Sicherung für Datenbank **A** aus. Fahren Sie mit Schritt 6 fort.  
  
6.  Stellen Sie die Sicherung von Datenbank **A** in der Datenbank **B** wieder her. Datenbank **B** verfügt nun über die Daten aus Datenbank **A**, nicht jedoch über die Replikationskonfiguration. Wenn Sie eine Sicherung auf einem anderen Server wiederherstellen, wird die Replikation entfernt. Folglich ist die Replikation nicht mehr in Datenbank **B** enthalten. Fahren Sie mit Schritt 7 fort.  
  
7.  Erstellen Sie die Veröffentlichung in Datenbank **B** neu, und erstellen Sie dann die Abonnements zwischen der Datenbank **A** und der Datenbank **B** neu. (Abonnements, die Datenbank **C** mit einbeziehen, werden in einem umfassenderen Schritt behandelt.).  
  
    1.  Erstellen Sie die Veröffentlichung in Datenbank **B** neu. Fahren Sie mit Schritt b fort.  
  
    2.  Erstellen Sie das Abonnement in Datenbank **B** für die Veröffentlichung in Datenbank **A**neu. Geben Sie dabei an, dass das Abonnement mit einer Sicherung initialisiert wird (ein Wert **initialize with backup** für den **@sync_type** -Parameter von [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Fahren Sie mit Schritt c fort.  
  
    3.  Erstellen Sie das Abonnement in Datenbank **A** für die Veröffentlichung in Datenbank **B**neu. Geben Sie dabei an, dass der Abonnent bereits über die Daten verfügt (ein Wert **replication support only** für den **@sync_type** -Parameter von [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Fahren Sie mit Schritt 8 fort.  
  
8.  Führen Sie die Verteilungs-Agents aus, und synchronisieren Sie die Abonnements in den Datenbanken **A** und **B**. Falls die veröffentlichten Tabellen Identitätsspalten enthalten, fahren Sie mit Schritt 9 fort. Wenn nicht, fahren Sie mit Schritt 10 fort.  
  
9. Nach der Wiederherstellung wird der Identitätsbereich, den Sie den Tabellen in Datenbank **A** zugewiesen haben, auch in Datenbank **B** verwendet. Stellen Sie sicher, dass die wiederhergestellte Datenbank **B** alle Änderungen aus der fehlerhaften Datenbank **B** empfangen hat, die an die Datenbanken **A** und **C** weitergegeben wurden. Weisen Sie dann den Identitätsbereich für jede Tabelle neu zu.  
  
    1.  Führen Sie [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) in der Datenbank **B** aus, und rufen Sie den Ausgabeparameter **@request_id**. Fahren Sie mit Schritt b fort.  
  
    2.  Der Verteilungs-Agent wird standardmäßig fortlaufend ausgeführt, folglich sollten Token automatisch an alle Knoten gesendet werden. Wenn der Verteilungs-Agent nicht im fortlaufenden Modus ausgeführt wird, führen Sie den Agent aus. Weitere Informationen finden Sie unter [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) oder [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md). Fahren Sie mit Schritt c fort.  
  
    3.  Führen Sie [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)unter Angabe des in Schritt B abgerufenen Werts für **@request_id** aus. Warten Sie, bis alle Knoten angeben, dass sie die Peeranforderung empfangen haben. Fahren Sie mit Schritt d fort.  
  
    4.  Verwenden Sie [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) , um den einzelnen Tabellen in Datenbank **B** neue Ausgangswerte zuzuweisen, um sicherzustellen, dass ein ordnungsgemäßer Bereich verwendet wird. Fahren Sie mit Schritt 10 fort.  
  
     Weitere Informationen zum Verwalten von Identitätsbereichen finden Sie im Abschnitt „Zuweisen von Bereichen für die manuelle Identitätsbereichsverwaltung“ unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
10. An diesem Punkt sind Datenbank **B** und Datenbank **C** nicht direkt verbunden, sie erhalten jedoch Änderungen über Datenbank **A**. Wenn die Topologie Knoten aufweist, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ausgeführt wird, fahren Sie mit Schritt 11 fort; andernfalls fahren Sie mit Schritt 12 fort.  
  
11. Versetzen Sie das System in einen inaktiven Status, und erstellen Sie dann das Abonnement zwischen Datenbank **B** und Datenbank **C** neu. Um das System in einen inaktiven Status zu versetzen, beenden Sie alle Aktivitäten an veröffentlichten Tabellen in allen Knoten, und stellen Sie sicher, dass jeder Knoten alle Änderungen aller anderen Knoten erhalten hat.  
  
    1.  Beenden Sie alle Aktivitäten an allen veröffentlichten Tabellen in der Peer-zu-Peer-Topologie. Fahren Sie mit Schritt b fort.  
  
    2.  Führen Sie [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) in der Datenbank **B** aus, und rufen Sie den Ausgabeparameter **@request_id**. Fahren Sie mit Schritt c fort.  
  
    3.  Der Verteilungs-Agent wird standardmäßig fortlaufend ausgeführt, folglich sollten Token automatisch an alle Knoten gesendet werden. Wenn der Verteilungs-Agent nicht im fortlaufenden Modus ausgeführt wird, führen Sie den Agent aus. Fahren Sie mit Schritt d fort.  
  
    4.  Führen Sie [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)unter Angabe des in Schritt B abgerufenen Werts für **@request_id** aus. Warten Sie, bis alle Knoten angeben, dass sie die Peeranforderung empfangen haben. Fahren Sie mit Schritt e fort.  
  
    5.  Erstellen Sie das Abonnement in Datenbank **B** für die Veröffentlichung in Datenbank **C**neu. Geben Sie dabei an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt b fort.  
  
    6.  Erstellen Sie das Abonnement in Datenbank **C** für die Veröffentlichung in Datenbank **B**neu. Geben Sie dabei an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt 13 fort.  
  
12. Erstellen Sie das Abonnement zwischen Datenbank **B** und Datenbank **C**neu:  
  
    1.  Fragen Sie in Datenbank **B**die [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) -Tabelle ab, um die Protokollfolgenummer (Log Sequence Number, LSN) der letzten Transaktion abzurufen, die Datenbank **B** von Datenbank **C**erhalten hat.  
  
    2.  Erstellen Sie das Abonnement in Datenbank **B** für die Veröffentlichung in Datenbank **C**neu. Geben Sie dabei an, dass das Abonnement basierend auf der LSN initialisiert wird (ein Wert **initialize from lsn** für den **@sync_type** -Parameter von [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Fahren Sie mit Schritt b fort.  
  
    3.  Erstellen Sie das Abonnement in Datenbank **C** für die Veröffentlichung in Datenbank **B**neu. Geben Sie dabei an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt 13 fort.  
  
13. Führen Sie die Verteilungs-Agents aus, und synchronisieren Sie die Abonnements in den Datenbanken **B** und **C**. Die Wiederherstellung ist abgeschlossen.  
  
#### <a name="msdb-database-publisher"></a>msdb-Datenbank (Verleger)  
  
1.  Stellen Sie die aktuellste Sicherung der **msdb** -Datenbank wieder her.  
  
2.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Erstellen Sie den Auftrag für ein Abonnementcleanup mithilfe der Replikationsskripts neu. Die Wiederherstellung ist abgeschlossen.  
  
#### <a name="master-database-publisher"></a>master-Datenbank (Verleger)  
  
1.  Stellen Sie die aktuellste Sicherung der **master** -Datenbank wieder her.  
  
2.  Stellen Sie sicher, dass die Datenbank hinsichtlich der Replikationskonfiguration und der Einstellungen mit der Veröffentlichungsdatenbank konsistent ist.  
  
### <a name="databases-at-the-distributor"></a>Datenbanken auf dem Verteiler  
  
#### <a name="distribution-database"></a>Verteilungsdatenbank  
  
1.  Stellen Sie die aktuellste Sicherung der Verteilungsdatenbank wieder her.  
  
2.  War die Einstellung **sync with backup** vor dem Fehler für die Verteilungsdatenbank aktiviert? Wenn ja, fahren Sie mit Schritt 3 fort, wenn nein, fahren Sie mit Schritt 4 fort.  
  
     Wenn die Einstellung aktiviert ist, gibt die Abfrage `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` den Wert 1 zurück.  
  
3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 4 fort.  
  
4.  Entweder sind die Konfigurationsinformationen in der wiederhergestellten Verteilungsdatenbank nicht aktuell, oder die Option **sync with backup** wurde nicht für die Verteilungsdatenbank festgelegt. (Nach der Wiederherstellung fehlen in der Verteilungsdatenbank möglicherweise Transaktionen, für die auf dem Verleger ein Commit ausgeführt wurde, die jedoch noch nicht an Abonnenten übermittelt wurden.) Löschen Sie die Replikation, und erstellen Sie sie neu. Führen Sie dann eine Überprüfung aus.  
  
    1.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt b fort.  
  
         Weitere Informationen zum Entfernen einer Replikation finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen zum Angeben, dass der Abonnement bereits über die Daten verfügt, finden Sie unter [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
    2.  Markieren Sie alle Veröffentlichungen zur Überprüfung. Initialisieren Sie alle Abonnements neu, bei denen die Überprüfung einen Fehler erzeugt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zur Überprüfung finden Sie unter [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md). Weitere Informationen zur Neuinitialisierung finden Sie unter [Erneutes Initialisieren von Abonnements](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="msdb-database-distributor"></a>msdb-Datenbank (Verteiler)  
  
1.  Stellen Sie die aktuellste Sicherung der **msdb** -Datenbank wieder her.  
  
2.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt 4 fort.  
  
     Weitere Informationen zum Entfernen einer Replikation finden Sie unter [sp_removedbreplication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
     Weitere Informationen zum Angeben, dass der Abonnement bereits über die Daten verfügt, finden Sie unter [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
4.  Markieren Sie alle Veröffentlichungen zur Überprüfung. Initialisieren Sie alle Abonnements neu, bei denen die Überprüfung einen Fehler erzeugt. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zur Überprüfung finden Sie unter [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md). Weitere Informationen zur Neuinitialisierung finden Sie unter [Erneutes Initialisieren von Abonnements](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### <a name="master-database-distributor"></a>master-Datenbank (Verteiler)  
  
1.  Stellen Sie die aktuellste Sicherung der **master** -Datenbank wieder her.  
  
2.  Stellen Sie sicher, dass die Datenbank hinsichtlich der Replikationskonfiguration und der Einstellungen mit der Veröffentlichungsdatenbank konsistent ist.  
  
### <a name="databases-at-the-subscriber"></a>Datenbanken auf dem Abonnenten  
  
#### <a name="subscription-database"></a>Abonnementdatenbank  
  
1.  Ist die letzte Sicherung der Abonnementdatenbank jünger als die Einstellung für die minimale Beibehaltungsdauer für die Verteilung der Verteilungsdatenbank? (Hiermit ermitteln Sie, ob der Verteiler noch über alle Befehle verfügt, die zum Aktualisieren des Abonnenten erforderlich sind.) Wenn ja, fahren Sie mit Schritt 2 fort. Wenn nein, initialisieren Sie das Abonnement erneut. Die Wiederherstellung ist abgeschlossen.  
  
     Um die Einstellung für die maximale Beibehaltungsdauer der Verteilung zu ermitteln, führen Sie [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) aus, und rufen Sie den Wert aus der **max_distretention** -Spalte ab (es handelt sich um einen Stundenwert).  
  
     Weitere Informationen zum erneuten Initialisieren eines Abonnements finden Sie unter [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
2.  Stellen Sie die aktuellste Sicherung der Abonnementdatenbank wieder her. Fahren Sie mit Schritt 3 fort.  
  
3.  Wenn die Abonnementdatenbank nur Pushabonnements enthält, fahren Sie mit Schritt 4 fort. Enthält die Abonnementdatenbank auch Pullabonnements, stellen Sie die folgenden Fragen: Sind die Abonnementinformationen aktuell? Sind in der Datenbank alle Tabellen und Optionen eingeschlossen, die beim Auftreten des Fehlers festgelegt waren? Wenn ja, fahren Sie mit Schritt 4 fort. Wenn nein, initialisieren Sie das Abonnement erneut. Die Wiederherstellung ist abgeschlossen.  
  
4.  Führen Sie den Verteilungs-Agent aus, um den Abonnenten zu synchronisieren. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zum Starten und Beenden eines Verteilungs-Agents finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
#### <a name="msdb-database-subscriber"></a>msdb-Datenbank (Abonnent)  
  
1.  Stellen Sie die aktuellste Sicherung der **msdb** -Datenbank wieder her. Werden Pullabonnements auf diesem Abonnenten verwendet? Wenn nicht, ist die Wiederherstellung abgeschlossen. Wenn ja, fahren Sie mit Schritt 2 fort.  
  
2.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Pullabonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Löschen Sie die Pullabonnements, und erstellen Sie sie neu. Geben Sie beim Neuerstellen der Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zum Löschen von Abonnements finden Sie unter [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
     Weitere Informationen zum Angeben, dass der Abonnement bereits über die Daten verfügt, finden Sie unter [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### <a name="master-database-subscriber"></a>master-Datenbank (Abonnent)  
  
1.  Stellen Sie die aktuellste Sicherung der **master** -Datenbank wieder her.  
  
2.  Stellen Sie sicher, dass die Datenbank hinsichtlich der Replikationskonfiguration und der Einstellungen mit der Veröffentlichungsdatenbank konsistent ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [Initialisieren eines Abonnements](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Synchronisieren von Daten](../../../relational-databases/replication/synchronize-data.md)  
  
  
