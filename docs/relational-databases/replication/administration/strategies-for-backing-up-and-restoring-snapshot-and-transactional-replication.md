---
title: "Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherungen [SQL Server-Replikation], Momentaufnahmereplikation"
  - "Wiederherstellen [SQL Server-Replikation], Transaktionsreplikation"
  - "Momentaufnahmereplikation [SQL Server], Sicherung und Wiederherstellung"
  - "Wiederherstellung [SQL Server-Replikation], Momentaufnahmereplikation"
  - "Wiederherstellen [SQL Server-Replikation], Transaktionsreplikation"
  - "Transaktionsreplikation, Sicherung und Wiederherstellung"
  - "Wiederherstellung [SQL Server-Replikation], Momentaufnahmereplikation"
  - "sync with backup [SQL Server-Replikation]"
  - "Sicherungen [SQL Server-Replikation], Transaktionsreplikation"
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation
  Drei Bereiche sind beim Entwickeln einer Sicherungs- und Wiederherstellungsstrategie für die Momentaufnahme- und Transaktionsreplikation zu berücksichtigen:  
  
-   Die zu sichernden Datenbanken.  
  
-   Die Sicherungseinstellungen für die Transaktionsreplikation.  
  
-   Die zum Wiederherstellen einer Datenbank erforderlichen Schritte. Diese hängen vom Typ der Replikation und den Optionen ab, der bzw. die ausgewählt werden.  
  
 In diesem Thema wird jeder dieser Bereiche in den nächsten drei Abschnitten erläutert. Informationen zum Sichern und Wiederherstellen bei Oracle-Verlegern finden Sie unter [Sicherung und Wiederherstellung für Oracle-Verleger](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md).  
  
## Sichern von Datenbanken  
 Sichern Sie bei der Momentaufnahme- und Transaktionsreplikation regelmäßig die folgenden Datenbanken:  
  
-   Veröffentlichungsdatenbank auf dem Verleger  
  
-   Verteilungsdatenbank auf dem Verteiler  
  
-   Abonnementdatenbank auf den einzelnen Abonnenten  
  
-   Die Systemdatenbanken **master** und **msdb** auf dem Verleger, Verteiler und allen Abonnenten. Diese Datenbanken sollten zur selben Zeit wie alle anderen Datenbanken und die entsprechende Replikationsdatenbank gesichert werden. Sichern Sie z. B. die **master** und **Msdb** Datenbanken auf dem Verleger zur gleichen Zeit die Sicherung der Veröffentlichungsdatenbank. Wenn die Veröffentlichungsdatenbank wiederhergestellt wird, stellen sicher, dass die **master** und **Msdb** hinsichtlich der Replikationskonfiguration und-Einstellungen mit der Veröffentlichungsdatenbank konsistent sind.  
  
 Wenn Sie regelmäßige Protokollsicherungen ausführen, sollten in den Protokollsicherungen auch alle replikationsrelevanten Änderungen erfasst werden. Wenn Sie keine Protokollsicherungen ausführen, sollte immer dann eine Sicherungskopie erstellt werden, wenn eine für die Replikation relevante Einstellung geändert wird. Weitere Informationen finden Sie unter [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## Sicherungseinstellungen für die Transaktionsreplikation  
 Transaktionsreplikation schließt die Verwendung der **Synchronisieren mit der Sicherung** Option, die für die Verteilungsdatenbank und die Veröffentlichungsdatenbank festgelegt werden kann:  
  
-   Es wird empfohlen, diese Option für die Verteilungsdatenbank immer festzulegen.  
  
     Mit dieser Option wird sichergestellt, dass Transaktionen im Protokoll der Veröffentlichungen nicht abgeschnitten werden, bevor sie in der Verteilungsdatenbank gesichert wurden. Die Verteilungsdatenbank kann auf die letzte Sicherung wiederhergestellt werden. Eventuell fehlende Transaktionen werden von der Veröffentlichungsdatenbank an die Verteilungsdatenbank übermittelt. Die Replikation wird ohne Einschränkungen fortgesetzt.  
  
     Das Festlegen dieser Option für die Verteilungsdatenbank wirkt sich nicht auf die Replikationslatenzzeit aus. Mit dem Festlegen dieser Option wird die Kürzung des Protokolls der Veröffentlichungsdatenbank so lange verzögert, bis die entsprechenden Transaktionen in der Verteilungsdatenbank gesichert sind. (Dies kann zur Erstellung eines umfangreicheren Transaktionsprotokolls in der Veröffentlichungsdatenbank führen.)  
  
-   Es wird empfohlen, diese Option für die Veröffentlichungsdatenbank festzulegen, falls die Anwendung eine zusätzliche Latenzzeit unterstützt.  
  
     Wenn Sie diese Option für die Veröffentlichungsdatenbank festlegen, stellen Sie sicher, dass Transaktionen erst an die Verteilungsdatenbank übermittelt werden, wenn Sie in der Veröffentlichungsdatenbank gesichert wurden. Die letzte Sicherung der Veröffentlichungsdatenbank kann dann auf dem Verleger wiederhergestellt werden, und es besteht keine Möglichkeit, dass die Verteilungsdatenbank Transaktionen enthält, die in der wiederhergestellten Veröffentlichungsdatenbank nicht vorhanden sind.  
  
     Latenzzeit und Durchsatz sind betroffen, da Transaktionen erst an die Verteilungsdatenbank übermittelt werden können, nachdem sie auf dem Verleger gesichert wurden. Wenn z. B. das Transaktionsprotokoll alle fünf Minuten gesichert wird, entsteht eine zusätzliche Latenzzeit von fünf Minuten zwischen dem Ausführen des Commit für eine Transaktion auf dem Verleger und dem Übermitteln der Transaktion an die Verteilungsdatenbank und anschließend an den Abonnenten.  
  
    > [!NOTE]  
    >  Die **Synchronisierung mit der Sicherung** Option gewährleistet die Konsistenz zwischen der Veröffentlichungsdatenbank und der Verteilungsdatenbank, aber die Option kein Garant gegen Datenverlust. Wenn z. B. das Transaktionsprotokoll verloren geht, sind Transaktionen, für die seit der letzten Sicherung des Transaktionsprotokolls ein Commit ausgeführt wurde, nicht in der Veröffentlichungsdatenbank oder der Verteilungsdatenbank verfügbar. Das ist das gleiche Verhalten wie bei einer nicht replizierten Datenbank.  
  
 **So legen Sie die Option sync with backup fest**  
  
-   Replikation [!INCLUDE[tsql](../../../includes/tsql-md.md)] programming: [Aktivieren koordinierter Sicherungen für Transaktionsreplikation & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/administration/enable coordinated backups for transactional replication.md)  
  
## Wiederherstellen der an der Replikation beteiligten Datenbanken   
 Wenn aktuelle Sicherungen verfügbar sind und die entsprechenden Schritte befolgt werden, können Sie alle Datenbanken einer Replikationstopologie wiederherstellen. Die Wiederherstellungsschritte für die Veröffentlichungsdatenbank hängen vom Typ der verwendeten Replikation und den verwendeten Optionen ab. Die Wiederherstellungsschritte für alle anderen Datenbanken sind jedoch vom Typ und den Optionen unabhängig.  
  
 Die Replikation ermöglicht das Wiederherstellen replizierter Datenbanken auf dem Server und in die Datenbank, die zum Erstellen der Sicherung herangezogen wurden. Wenn Sie eine Sicherungskopie einer replizierten Datenbank auf einem anderen Server bzw. in einer anderen Datenbank wiederherstellen, können Replikationseinstellungen nicht beibehalten werden. In diesem Fall müssen nach der Wiederherstellung der Sicherungskopien sämtliche Veröffentlichungen und Abonnements neu erstellt werden.  
  
### Verleger  
 Wiederherstellungsschritte werden für die folgenden Replikationstypen bereitgestellt:  
  
-   Momentaufnahmereplikation  
  
-   Schreibgeschützte Transaktionsreplikation  
  
-   Transaktionsreplikation mit Updateabonnements  
  
-   Peer-zu-Peer-Transaktionsreplikation  
  
 Die Wiederherstellung der **Msdb** und **master** -Datenbanken, die auch in diesem Abschnitt behandelt werden, ist für alle vier Typen gleich.  
  
#### Veröffentlichungsdatenbank: Momentaufnahmereplikation  
  
1.  Stellen Sie die aktuellste Sicherung der Veröffentlichungsdatenbank wieder her. Fahren Sie mit Schritt 2 fort.  
  
2.  Enthält die Sicherung der Veröffentlichungsdatenbank die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zum Entfernen der Replikation finden Sie unter [Sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
#### Veröffentlichungsdatenbank: Schreibgeschützte Transaktionsreplikation  
  
1.  Stellen Sie die aktuellste Sicherung der Veröffentlichungsdatenbank wieder her. Fahren Sie mit Schritt 2 fort.  
  
2.  Wurde die **Synchronisierung mit der Sicherung** Einstellung für die Veröffentlichungsdatenbank vor Auftreten des Fehlers aktiviert? Wenn ja, fahren Sie mit Schritt 3 fort, wenn nein, fahren Sie mit Schritt 5 fort.  
  
     Wenn die Einstellung aktiviert ist, gibt die Abfrage `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` den Wert 1 zurück.  
  
3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 4 fort.  
  
4.  Die Konfigurationsinformationen in der wiederhergestellten Veröffentlichungsdatenbank sind nicht aktuell. Deshalb müssen Sie sicherstellen, dass die Abonnenten alle ausstehenden Befehle in der Verteilungsdatenbank aufweisen. Löschen Sie anschließend die Replikationskonfiguration, und erstellen Sie sie erneut.  
  
    1.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Stellen Sie sicher, dass alle Befehle an die Abonnenten übermittelt werden die **nicht verteilte Befehle** Registerkarte im Replikationsmonitor oder durch Abfragen der [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) Ansicht in der Verteilungsdatenbank. Fahren Sie mit Schritt b fort.  
  
         Weitere Informationen zum Ausführen der Verteilungsagent finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Weitere Informationen zum Überprüfen von Befehlen finden Sie unter [Ansicht replizierte Befehle und andere Informationen in der Verteilungsdatenbank & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
    2.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zum Entfernen der Replikation finden Sie unter [Sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen dazu, wie Sie angeben, dass der Abonnent bereits über Daten verfügt, finden Sie unter [ein Abonnement manuell initialisiert](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
5.  Die **Synchronisierung mit der Sicherung** Option wurde nicht für die Veröffentlichungsdatenbank festgelegt. Deshalb wurden Transaktionen, die nicht in die wiederhergestellte Sicherung eingeschlossen waren, möglicherweise an den Verteiler und die Abonnenten übermittelt. Stellen Sie nun sicher, dass die Abonnenten über alle ausstehenden Befehle in der Verteilungsdatenbank verfügen. Wenden Sie dann manuell alle Transaktionen auf die Veröffentlichungsdatenbank an, die nicht in die wiederhergestellte Sicherung eingeschlossen waren.  
  
    > [!IMPORTANT]  
    >  Beim Ausführen dieses Prozesses kann es passieren, dass veröffentlichte Tabellen auf einen Stand wiederhergestellt werden, der vor dem Stand anderer nicht veröffentlichter Tabellen liegt, die aus der Sicherung wiederhergestellt werden.  
  
    1.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Stellen Sie sicher, dass alle Befehle an die Abonnenten übermittelt werden die **nicht verteilte Befehle** Registerkarte im Replikationsmonitor oder durch Abfragen der [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) Ansicht in der Verteilungsdatenbank. Fahren Sie mit Schritt b fort.  
  
         Weitere Informationen zum Ausführen der Verteilungsagent finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Weitere Informationen zum Überprüfen von Befehlen finden Sie unter [Ansicht replizierte Befehle und andere Informationen in der Verteilungsdatenbank & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
    2.  Verwenden der [Dienstprogramm Tablediff](../../../tools/tablediff-utility.md) oder ein anderes Tool für den Verleger manuell mit dem Abonnenten zu synchronisieren. So können Sie Daten aus der Abonnementdatenbank wiederherstellen, die nicht in der Sicherung der Veröffentlichungsdatenbank enthalten waren. Fahren Sie mit Schritt c fort.  
  
         Weitere Informationen zu den **Tablediff** -Dienstprogramm finden Sie unter [Vergleichen replizierten Tabellen für Unterschiede & #40; Replikationsprogrammierung & #41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn Ja, führen die [Sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) gespeicherte Prozedur auf die Verleger Metadaten erneut mit der Verteiler synchronisieren. Die Wiederherstellung ist abgeschlossen. Wenn nein, fahren Sie mit Schritt d fort.  
  
    4.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zum Entfernen der Replikation finden Sie unter [Sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen dazu, wie Sie angeben, dass der Abonnent bereits über Daten verfügt, finden Sie unter [ein Abonnement manuell initialisiert](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Veröffentlichungsdatenbank: Transaktionsreplikation mit Updateabonnements  
  
1.  Stellen Sie die aktuellste Sicherung der Veröffentlichungsdatenbank wieder her. Fahren Sie mit Schritt 2 fort.  
  
2.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Stellen Sie sicher, dass alle Befehle an die Abonnenten übermittelt werden die **nicht verteilte Befehle** Registerkarte im Replikationsmonitor oder durch Abfragen der [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) Ansicht in der Verteilungsdatenbank. Fahren Sie mit Schritt 3 fort.  
  
     Weitere Informationen zum Ausführen der Verteilungsagent finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
     Weitere Informationen zum Überprüfen von Befehlen finden Sie unter [Ansicht replizierte Befehle und andere Informationen in der Verteilungsdatenbank & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
3.  Bei Verwendung von Abonnements mit verzögertem an jeden Abonnenten herstellen und löschen Sie alle Zeilen aus der [MSreplication_queue & #40; Transact-SQL & #41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) die Tabelle in der Abonnementdatenbank. Fahren Sie mit Schritt 4 fort.  
  
    > [!NOTE]  
    >  Wenn Sie Abonnements mit verzögertem Update über eine Warteschlange verwenden und Tabellen Identitätsspalten enthalten, müssen Sie sicherstellen, dass nach jeder Wiederherstellung die richtigen Identitätsbereiche zugewiesen werden. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
4.  Stellen Sie nun sicher, dass die Abonnenten über alle ausstehenden Befehle in der Verteilungsdatenbank verfügen. Wenden Sie dann manuell alle Transaktionen auf die Veröffentlichungsdatenbank an, die nicht in die wiederhergestellte Sicherung eingeschlossen waren.  
  
    > [!IMPORTANT]  
    >  Beim Ausführen dieses Prozesses kann es passieren, dass veröffentlichte Tabellen auf einen Stand wiederhergestellt werden, der vor dem Stand anderer nicht veröffentlichter Tabellen liegt, die aus der Sicherung wiederhergestellt werden.  
  
    1.  Führen Sie den Verteilungs-Agent aus, bis alle Abonnenten mit den ausstehenden Befehlen in der Verteilungsdatenbank synchronisiert wurden. Stellen Sie sicher, dass alle Befehle an die Abonnenten gesendet werden, mithilfe des Replikationsmonitors oder Abfragen der [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) Ansicht in der Verteilungsdatenbank. Fahren Sie mit Schritt b fort.  
  
    2.  Verwenden der [Tablediff (Hilfsprogramm)](../../../tools/tablediff-utility.md) oder ein anderes Tool für den Verleger manuell mit dem Abonnenten zu synchronisieren. So können Sie Daten aus der Abonnementdatenbank wiederherstellen, die nicht in der Sicherung der Veröffentlichungsdatenbank enthalten waren. Fahren Sie mit Schritt c fort.  
  
         Weitere Informationen zu den **Tablediff** -Dienstprogramm finden Sie unter [Vergleichen replizierten Tabellen für Unterschiede & #40; Replikationsprogrammierung & #41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn Ja, führen die [Sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) gespeicherte Prozedur auf die Verleger Metadaten erneut mit der Verteiler synchronisieren. Die Wiederherstellung ist abgeschlossen. Wenn nein, fahren Sie mit Schritt d fort.  
  
    4.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zum Entfernen der Replikation finden Sie unter und [Sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen dazu, wie Sie angeben, dass der Abonnent bereits über Daten verfügt, finden Sie unter [ein Abonnement manuell initialisiert](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Veröffentlichungsdatenbank: Peer-zu-Peer-Transaktionsreplikation  
 In den folgenden Schritten Publikationsdatenbanken **ein**, **B**, und **C** befinden sich in einer Peer-to-Peer-transaktionsreplikationstopologie. Datenbanken **ein** und **C** sind online und funktionieren ordnungsgemäß; Datenbank **B** ist die Datenbank wiederhergestellt werden soll. Der hier beschriebene Prozess, insbesondere die Schritte 7, 10 und 11, ist vergleichbar mit dem Prozess zum Hinzufügen eines Knotens zu einer Peer-zu-Peer-Topologie. Die einfachste Möglichkeit zum Ausführen dieser Schritte ist diejenige mithilfe des Assistenten zum Konfigurieren der Peer-zu-Peer-Topologie. Sie können jedoch auch gespeicherte Prozeduren dafür verwenden.  
  
1.  Führen Sie die Verteilung Agents zum Synchronisieren von Abonnements in den Datenbanken **ein** und **C**. Fahren Sie mit Schritt 2 fort.  
  
     Weitere Informationen zum Ausführen der Verteilungsagent finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Wenn die Verteilungsdatenbank **B** verwendet immer noch verfügbar ist, führen Verteilungs-Agents zum Synchronisieren der Abonnements zwischen Datenbanken **B** und **ein** und den Datenbanken B und **C**. Fahren Sie mit Schritt 3 fort.  
  
3.  Entfernen von Metadaten aus der Datenbank, die **B** verwendeten [Sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md) in der Verteilungsdatenbank für **B**. Fahren Sie mit Schritt 4 fort.  
  
4.  In den Datenbanken **ein** und **C**, löschen Sie die Abonnements für die Veröffentlichung in Datenbank **B**. Fahren Sie mit Schritt 5 fort.  
  
     Weitere Informationen zum Löschen von Abonnements finden Sie unter [abonnieren Publikationen](../../../relational-databases/replication/subscribe-to-publications.md).  
  
5.  Führen Sie eine Sicherung oder eine vollständige Sicherung der Datenbank **ein**. Fahren Sie mit Schritt 6 fort.  
  
6.  Wiederherstellen der Sicherung der Datenbank **ein** in Datenbank **B**. Datenbank **B** verfügt jetzt über die Daten aus der Datenbank **ein**, nicht jedoch die Replikationskonfiguration. Wenn Sie eine Sicherung auf einem anderen Server wiederherstellen, wird die Replikation entfernt. aus diesem Grund wurde Replikation aus der Datenbank entfernt **B**. Fahren Sie mit Schritt 7 fort.  
  
7.  Erstellen Sie die Veröffentlichung in Datenbank **B**, und dann erneut erstellen Abonnements zwischen Datenbanken **ein** und **B**. (Abonnements, die Datenbank betreffen **C** zu einem späteren Zeitpunkt verarbeitet werden.).  
  
    1.  Erstellen Sie die Veröffentlichung in Datenbank **B**. Fahren Sie mit Schritt b fort.  
  
    2.  Erneutes Erstellen des Abonnements in der Datenbank **B** für die Veröffentlichung in Datenbank **ein**, gibt an, dass das Abonnement mit einer Sicherung initialisiert werden soll (Wert **Initialisieren mit Sicherung** für die **@sync_type** Parameter [Sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Fahren Sie mit Schritt c fort.  
  
    3.  Das Abonnement in Datenbank neu erstellen **ein** für die Veröffentlichung in Datenbank **B**, gibt an, dass der Abonnent bereits über Daten verfügt (der Wert **nur replikationsunterstützung** für die **@sync_type** Parameter der [Sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Fahren Sie mit Schritt 8 fort.  
  
8.  Führen Sie die Verteilung Agents zum Synchronisieren von Abonnements in den Datenbanken **ein** und **B**. Falls die veröffentlichten Tabellen Identitätsspalten enthalten, fahren Sie mit Schritt 9 fort. Wenn nicht, fahren Sie mit Schritt 10 fort.  
  
9. Nach der Wiederherstellung der Identitätsbereich, den Sie für jede Tabelle in der Datenbank zugewiesen **ein** würde auch in der Datenbank verwendet werden **B**. Stellen Sie sicher, dass die wiederhergestellte Datenbank **B** Alle Änderungen aus der fehlerhaften Datenbank empfangen hat **B** weitergegeben wurden in Datenbank **ein** und Datenbank **C**; und weisen Sie dann den Identitätsbereich für jede Tabelle neu.  
  
    1.  Führen Sie [Sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) Datenbank **B** und rufen die Ausgabeparameter **@request_id**. Fahren Sie mit Schritt b fort.  
  
    2.  Der Verteilungs-Agent wird standardmäßig fortlaufend ausgeführt, folglich sollten Token automatisch an alle Knoten gesendet werden. Wenn der Verteilungs-Agent nicht im fortlaufenden Modus ausgeführt wird, führen Sie den Agent aus. Weitere Informationen finden Sie unter [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) oder [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md). Fahren Sie mit Schritt c fort.  
  
    3.  Führen Sie [Sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), unter Angabe der **@request_id** in Schritt b abgerufenen Werts. Warten Sie, bis alle Knoten angeben, dass sie die Peeranforderung empfangen haben. Fahren Sie mit Schritt d fort.  
  
    4.  Verwendung [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) jede Tabelle in der Datenbank durch Seeding erneut einrichten **B** sicherstellen, dass ein ordnungsgemäßer Bereich verwendet wird. Fahren Sie mit Schritt 10 fort.  
  
     Weitere Informationen über das Verwalten von Identitätsbereichen finden Sie im Abschnitt "Zuweisen von Bereichen für die manuelle identitätsbereichsverwaltung" von [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
10. An diesem Punkt sind Datenbank **B** und Datenbank **C** nicht direkt verbunden, sie erhalten jedoch Änderungen über Datenbank **ein**. Wenn die Topologie Knoten aufweist, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ausgeführt wird, fahren Sie mit Schritt 11 fort; andernfalls fahren Sie mit Schritt 12 fort.  
  
11. Versetzen Sie das System, und erstellen dann das Abonnement zwischen Datenbank neu **B** und **C**. Um das System in einen inaktiven Status zu versetzen, beenden Sie alle Aktivitäten an veröffentlichten Tabellen in allen Knoten, und stellen Sie sicher, dass jeder Knoten alle Änderungen aller anderen Knoten erhalten hat.  
  
    1.  Beenden Sie alle Aktivitäten an allen veröffentlichten Tabellen in der Peer-zu-Peer-Topologie. Fahren Sie mit Schritt b fort.  
  
    2.  Führen Sie [Sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) Datenbank **B** und rufen die Ausgabeparameter **@request_id**. Fahren Sie mit Schritt c fort.  
  
    3.  Der Verteilungs-Agent wird standardmäßig fortlaufend ausgeführt, folglich sollten Token automatisch an alle Knoten gesendet werden. Wenn der Verteilungs-Agent nicht im fortlaufenden Modus ausgeführt wird, führen Sie den Agent aus. Fahren Sie mit Schritt d fort.  
  
    4.  Führen Sie [Sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), unter Angabe der **@request_id** in Schritt b abgerufenen Werts. Warten Sie, bis alle Knoten angeben, dass sie die Peeranforderung empfangen haben. Fahren Sie mit Schritt e fort.  
  
    5.  Erneutes Erstellen des Abonnements in der Datenbank **B** für die Veröffentlichung in Datenbank **C**, gibt an, dass der Abonnent bereits über Daten verfügt. Fahren Sie mit Schritt b fort.  
  
    6.  Erneutes Erstellen des Abonnements in der Datenbank **C** für die Veröffentlichung in Datenbank **B**, gibt an, dass der Abonnent bereits über Daten verfügt. Fahren Sie mit Schritt 13 fort.  
  
12. Erneutes Erstellen des Abonnements zwischen Datenbanken **B** und **C**:  
  
    1.  In der Datenbank **B**, Abfrage der [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) Tabelle rufen Sie die Protokollsequenznummer (LSN) der letzten Transaktion dieser Datenbank **B** aus der Datenbank empfangen hat **C**.  
  
    2.  Erneutes Erstellen des Abonnements in der Datenbank **B** für die Veröffentlichung in Datenbank **C**, gibt an, dass das Abonnement initialisiert werden soll, basierend auf der LSN (Wert **Initialisieren von Lsn** für die **@sync_type** Parameter [Sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Fahren Sie mit Schritt b fort.  
  
    3.  Erneutes Erstellen des Abonnements in der Datenbank **C** für die Veröffentlichung in Datenbank **B**, gibt an, dass der Abonnent bereits über Daten verfügt. Fahren Sie mit Schritt 13 fort.  
  
13. Führen Sie die Verteilung Agents zum Synchronisieren von Abonnements in den Datenbanken **B** und **C**. Die Wiederherstellung ist abgeschlossen.  
  
#### msdb-Datenbank (Verleger)  
  
1.  Wiederherstellen die letzten Sicherung der der **Msdb** Datenbank.  
  
2.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Erstellen Sie den Auftrag für ein Abonnementcleanup mithilfe der Replikationsskripts neu. Die Wiederherstellung ist abgeschlossen.  
  
#### master-Datenbank (Verleger)  
  
1.  Wiederherstellen die letzten Sicherung der der **master** Datenbank.  
  
2.  Stellen Sie sicher, dass die Datenbank hinsichtlich der Replikationskonfiguration und der Einstellungen mit der Veröffentlichungsdatenbank konsistent ist.  
  
### Datenbanken auf dem Verteiler  
  
#### Verteilungsdatenbank  
  
1.  Stellen Sie die aktuellste Sicherung der Verteilungsdatenbank wieder her.  
  
2.  Wurde die **Synchronisierung mit der Sicherung** Einstellung für die Verteilungsdatenbank vor Auftreten des Fehlers aktiviert? Wenn ja, fahren Sie mit Schritt 3 fort, wenn nein, fahren Sie mit Schritt 4 fort.  
  
     Wenn die Einstellung aktiviert ist, gibt die Abfrage `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` den Wert 1 zurück.  
  
3.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 4 fort.  
  
4.  Entweder die Konfigurationsinformationen in der wiederhergestellten Verteilungsdatenbank ist nicht aktuell, oder die **Synchronisierung mit der Sicherung** Option wurde nicht für die Verteilungsdatenbank festgelegt. (Nach der Wiederherstellung fehlen in der Verteilungsdatenbank möglicherweise Transaktionen, für die auf dem Verleger ein Commit ausgeführt wurde, die jedoch noch nicht an Abonnenten übermittelt wurden.) Löschen Sie die Replikation, und erstellen Sie sie neu. Führen Sie dann eine Überprüfung aus.  
  
    1.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt b fort.  
  
         Weitere Informationen zum Entfernen der Replikation finden Sie unter [Sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Weitere Informationen dazu, wie Sie angeben, dass der Abonnent bereits über Daten verfügt, finden Sie unter [ein Abonnement manuell initialisiert](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
    2.  Markieren Sie alle Veröffentlichungen zur Überprüfung. Initialisieren Sie alle Abonnements neu, bei denen die Überprüfung einen Fehler erzeugt. Die Wiederherstellung ist abgeschlossen.  
  
         Weitere Informationen zur Überprüfung finden Sie unter [Überprüfen von replizierten Daten](../../../relational-databases/replication/validate-replicated-data.md). Weitere Informationen zur neuinitialisierung finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### msdb-Datenbank (Verteiler)  
  
1.  Wiederherstellen die letzten Sicherung der der **Msdb** Datenbank.  
  
2.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Veröffentlichungen und Abonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Entfernen Sie die Replikationskonfiguration vom Verleger, vom Verteiler und von den Abonnenten, und erstellen Sie die Konfiguration dann neu. Geben Sie beim Neuerstellen von Abonnements an, dass der Abonnent bereits über die Daten verfügt. Fahren Sie mit Schritt 4 fort.  
  
     Weitere Informationen zum Entfernen der Replikation finden Sie unter [Sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
     Weitere Informationen dazu, wie Sie angeben, dass der Abonnent bereits über Daten verfügt, finden Sie unter [ein Abonnement manuell initialisiert](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
4.  Markieren Sie alle Veröffentlichungen zur Überprüfung. Initialisieren Sie alle Abonnements neu, bei denen die Überprüfung einen Fehler erzeugt. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zur Überprüfung finden Sie unter [Überprüfen von replizierten Daten](../../../relational-databases/replication/validate-replicated-data.md). Weitere Informationen zur neuinitialisierung finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### master-Datenbank (Verteiler)  
  
1.  Wiederherstellen die letzten Sicherung der der **master** Datenbank.  
  
2.  Stellen Sie sicher, dass die Datenbank hinsichtlich der Replikationskonfiguration und der Einstellungen mit der Veröffentlichungsdatenbank konsistent ist.  
  
### Datenbanken auf dem Abonnenten  
  
#### Abonnementdatenbank  
  
1.  Ist die letzte Sicherung der Abonnementdatenbank jünger als die Einstellung für die minimale Beibehaltungsdauer für die Verteilung der Verteilungsdatenbank? (Hiermit ermitteln Sie, ob der Verteiler noch über alle Befehle verfügt, die zum Aktualisieren des Abonnenten erforderlich sind.) Wenn ja, fahren Sie mit Schritt 2 fort. Wenn nein, initialisieren Sie das Abonnement erneut. Die Wiederherstellung ist abgeschlossen.  
  
     Führen Sie zum Bestimmen der maximalen Beibehaltungsdauer [Sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) und Abrufen des Werts aus der **Max_distretention** Spalte (dieser Wert wird in Stunden).  
  
     Weitere Informationen zum erneuten Initialisieren eines Abonnements finden Sie unter [erneutes Initialisieren eines Abonnements](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
2.  Stellen Sie die aktuellste Sicherung der Abonnementdatenbank wieder her. Fahren Sie mit Schritt 3 fort.  
  
3.  Wenn die Abonnementdatenbank nur Pushabonnements enthält, fahren Sie mit Schritt 4 fort. Enthält die Abonnementdatenbank auch Pullabonnements, stellen Sie die folgenden Fragen: Sind die Abonnementinformationen aktuell? Sind in der Datenbank alle Tabellen und Optionen eingeschlossen, die beim Auftreten des Fehlers festgelegt waren? Wenn ja, fahren Sie mit Schritt 4 fort. Wenn nein, initialisieren Sie das Abonnement erneut. Die Wiederherstellung ist abgeschlossen.  
  
4.  Führen Sie den Verteilungs-Agent aus, um den Abonnenten zu synchronisieren. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zum Ausführen der Verteilungsagent finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
#### msdb-Datenbank (Abonnent)  
  
1.  Wiederherstellen die letzten Sicherung der der **Msdb** Datenbank. Werden Pullabonnements auf diesem Abonnenten verwendet? Wenn nicht, ist die Wiederherstellung abgeschlossen. Wenn ja, fahren Sie mit Schritt 2 fort.  
  
2.  Ist die wiederhergestellte Sicherung vollständig und aktuell? Enthält sie die aktuelle Konfiguration für alle Pullabonnements? Wenn ja, ist die Wiederherstellung abgeschlossen. Wenn nein, fahren Sie mit Schritt 3 fort.  
  
3.  Löschen Sie die Pullabonnements, und erstellen Sie sie neu. Geben Sie beim Neuerstellen der Abonnements an, dass der Abonnent bereits über die Daten verfügt. Die Wiederherstellung ist abgeschlossen.  
  
     Weitere Informationen zum Löschen von Abonnements finden Sie unter [abonnieren Publikationen](../../../relational-databases/replication/subscribe-to-publications.md).  
  
     Weitere Informationen dazu, wie Sie angeben, dass der Abonnent bereits über Daten verfügt, finden Sie unter [ein Abonnement manuell initialisiert](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### master-Datenbank (Abonnent)  
  
1.  Wiederherstellen die letzten Sicherung der der **master** Datenbank.  
  
2.  Stellen Sie sicher, dass die Datenbank hinsichtlich der Replikationskonfiguration und der Einstellungen mit der Veröffentlichungsdatenbank konsistent ist.  
  
## Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Konfigurieren der Verteilung](../../../relational-databases/replication/configure-distribution.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)   
 [Initialisieren eines Abonnements](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Synchronisieren von Daten](../../../relational-databases/replication/synchronize-data.md)  
  
  