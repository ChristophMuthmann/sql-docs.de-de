---
title: "Verbessern der allgemeinen Replikationsleistung | Microsoft Docs"
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
  - "Veröffentlichungen [SQL Server-Replikation], Entwurf und Leistung"
  - "Entwerfen von Datenbanken [SQL Server], Replikationsleistung"
  - "Momentaufnahme-Agent, Leistung"
  - "Momentaufnahmen [SQL Server-Replikation], Leistungsaspekte"
  - "Mergereplikationsleistung [SQL Server-Replikation]"
  - "Momentaufnahmereplikation [SQL Server], Leistung"
  - "Abonnements [SQL Server-Replikation], Leistungsaspekte"
  - "Agents [SQL Server-Replikation], Leistung"
  - "Leistung [SQL Server-Replikation], allgemeine Überlegungen"
  - "Transaktionsreplikation, Leistung"
ms.assetid: 895b1ad7-ffb9-4a5c-bda6-e1dfbd56d9bf
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Verbessern der allgemeinen Replikationsleistung
  Wenn Sie die Hinweise in diesem Thema beachten, können Sie die allgemeine Leistung aller Replikationstypen in der Anwendung und im Netzwerk verbessern.  
  
## Server und Netzwerk  
  
-   Legen Sie den minimalen und maximalen Arbeitsspeichers [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].  
  
     Standardmäßig ändert [!INCLUDE[ssDE](../../../includes/ssde-md.md)] die Arbeitsspeicheranforderungen auf der Grundlage der verfügbaren Systemressourcen dynamisch. Um während Replikationsaktivitäten nur wenig Arbeitsspeicher zu vermeiden, verwenden Sie die **min Server Memory** Option, um die verfügbaren Speichers festzulegen. Um zu vermeiden, dass das Betriebssystem Speicher auslagern muss, können Sie auch ein maximum an Arbeitsspeicher mit Festlegen der **Max. Serverarbeitsspeicher** Option. Weitere Informationen finden Sie unter [Server Memory Serverkonfigurationsoptionen](../../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
-   Stellen Sie eine ordnungsgemäße Zuordnung der Datenbankdateien und Protokolldateien sicher. Verwenden Sie ein separates Laufwerk für das Transaktionsprotokoll für alle an der Replikation beteiligten Datenbanken.  
  
     Sie können die Zeit verringern, die zum Schreiben von Transaktionen benötigt wird, indem Sie die Protokolldateien auf ein anderes Laufwerk schreiben als das, das zum Speichern der Datenbank verwendet wird. Dieses Laufwerk kann mithilfe eines RAID 1-Gerätes (Redundant Array of Inexpensive Disks) gespiegelt werden, wenn Fehlertoleranz erforderlich ist. Verwenden Sie RAID 0 oder 0+1 (je nach Bedarf an Fehlertoleranz) für andere Datenbankdateien. Dies wird empfohlen, unabhängig davon, ob die Replikation verwendet wird.  
  
-   Fügen Sie gegebenenfalls Arbeitsspeicher für die Server hinzu, die für die Replikation verwendet werden, insbesondere für den Verteiler.  
  
-   Verwenden Sie Computer mit mehreren Prozessoren.  
  
     Replikations-Agents können von weiteren Prozessoren auf dem Server profitieren. Bei hoher CPU-Nutzung sollten Sie die Installation einer schnelleren CPU oder mehrerer CPUs in Betracht ziehen.  
  
-   Verwenden Sie ein schnelles Netzwerk.  
  
     Das Netzwerk kann besonders bei der Transaktionsreplikation einen erheblichen Leistungsengpass darstellen. Die Weitergabe von Änderungen an den Abonnenten kann deutlich beschleunigt werden, wenn Sie ein sehr schnelles Netzwerk mit 100 MBit/s oder mehr verwenden. Geben Sie bei einem langsamen Netzwerk geeignete Netzwerkeinstellungen und Agentparameter an.  
  
## Datenbankentwurf  
  
-   Beachten Sie die bewährten Methoden für den Datenbankentwurf.  
  
     Eine Leistungsoptimierung wirkt sich auf eine replizierte Datenbank genauso vorteilhaft aus wie auf eine nicht replizierte Datenbank. Indizes sind auf dem Abonnenten jedoch mit Bedacht zu verwenden: die Primärschlüsselspalte auf dem Abonnenten sollte indiziert werden, doch weitere Indizes können sich auf die Leistung beim Einfügen, Aktualisieren und Löschen auswirken.  
  
-   Legen Sie gegebenenfalls die Datenbankoption READ_COMMITTED_SNAPSHOT fest.  
  
     Um Konflikte zwischen der Benutzeraktivität und der Aktivität des Replikations-Agents besser vermeiden zu können, legen Sie diese Option für die Veröffentlichungs- und Abonnementdatenbanken fest:  
  
    ```  
    ALTER DATABASE AdventureWorks  
    SET READ_COMMITTED_SNAPSHOT ON  
    ```  
  
     Weitere Informationen finden Sie unter [ALTER DATABASE & #40; Transact-SQL & #41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Gehen Sie bei der Anwendungslogik in Triggern mit Bedacht vor.  
  
     Die Geschäftslogik in benutzerdefinierten Triggern auf dem Abonnenten kann die Replikation von Änderungen an den Abonnenten verlangsamen.  
  
    -   Für die Transaktionsreplikation kann es effizienter sein, diese Logik in benutzerdefinierte gespeicherte Prozeduren aufzunehmen, die für die Ausführung der replizierten Befehle verwendet werden. Weitere Informationen finden Sie unter [angeben, wie Änderungen für Transaktionsartikel weitergegeben werden](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
    -   Für die Mergereplikation kann es effizienter sein, Geschäftslogikhandler zu verwenden. Weitere Informationen finden Sie unter [führen Business Logic During Merge Synchronization](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
     Wenn Sie zur Wahrung der referenziellen Integrität Trigger in Tabellen verwenden, die für die Mergereplikation veröffentlicht werden, geben Sie die Verarbeitungsreihenfolge der Tabellen an. Auf diese Weise reduzieren Sie die Zahl der Wiederholungsversuche für den Merge-Agent. Weitere Informationen finden Sie unter [Geben Sie die Verarbeitung Reihenfolge von Merge Artikel](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
-   Schränken Sie die Verwendung des LOB-Datentyps (Large OBjects) ein.  
  
     LOBs beanspruchen mehr Speicherplatz und Verarbeitungszeit als andere Spaltendatentypen. Verwenden Sie diese Spalten nur dann in Artikeln, wenn sie für die Anwendung erforderlich sind. Die Datentypen **Text**, **Ntext**, und **Image** sind veraltet. Falls Sie LOBs einschließen, wir empfehlen die Verwendung von Datentypen **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, bzw..  
  
     Bei der Transaktionsreplikation sollten Sie mithilfe der Agent-Profil namens **für OLE DB-streaming**. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## Veröffentlichungsentwurf  
  
-   Veröffentlichen Sie nur die erforderlichen Daten.  
  
     Da die Replikation problemlos eingerichtet werden kann, gibt es eine Tendenz, mehr Daten zu veröffentlichen, als tatsächlich erforderlich sind. Dies kann weitere Ressourcen innerhalb der Verteilungsdatenbanken und Momentaufnahmedateien beanspruchen und den Durchsatz für erforderliche Dateien verringern. Sie sollten vermeiden, nicht benötigte Tabellen zu veröffentlichen, und in Betracht ziehen, Veröffentlichungen weniger häufig zu aktualisieren.  
  
-   Minimieren Sie Konflikte über den Veröffentlichungsentwurf und das Anwendungsverhalten.  
  
     Die folgenden Replikationstypen lassen Datenänderungen auf Abonnenten zu: Mergereplikation, Transaktionsreplikation mit aktualisierbaren Abonnements und Peer-zu-Peer-Transaktionsreplikation. Die Mergereplikation und die Transaktionsreplikation mit aktualisierbaren Abonnements unterstützen Datenkonflikte, wenn eine bestimmte Zeile zwischen Synchronisierungen in mehreren Knoten aktualisiert wird. Die Peer-zu-Peer-Replikation unterstützt keine Datenkonflikte; Datenänderungen müssen partitioniert werden. Unabhängig vom Typ der verwendeten Replikation wird empfohlen, Änderungen möglichst zu partitionieren, da dies den Verarbeitungsaufwand bei der Konflikterkennung und -lösung reduziert.  
  
     Sie können Änderungen partitionieren, indem Sie Datenteilmengen auf jedem Abonnenten veröffentlichen, oder indem eine Anwendung Änderungen für eine bestimmte Zeile an einen bestimmten Knoten leitet:  
  
    -   Die Mergereplikation unterstützt das Veröffentlichen von Datenteilmengen, indem parametrisierte Filter mit einzelnen Veröffentlichungen verwendet werden. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
    -   Die Transaktionsreplikation unterstützt das Veröffentlichen von Datenteilmengen, indem statische Filter mit mehreren Veröffentlichungen verwendet werden. Weitere Informationen finden Sie unter [veröffentlichten Filterdaten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Verwenden Sie Zeilenfilter mit Umsicht.  
  
     Enthält eine Transaktionsveröffentlichung einen oder mehrere Artikel mit Zeilenfiltern, muss der Protokolllese-Agent beim Scannen des Transaktionsprotokolls die Filter auf jede Zeile anwenden, die von einem Update der Tabelle betroffen sind. Das wirkt sich auf den Durchsatz des Protokolllese-Agents aus.  
  
     In ähnlicher Form muss die Mergereplikation geänderte oder gelöschte Zeilen auswerten, um die Abonnenten zu ermitteln, die diese Zeilen erhalten sollten. Wenn Zeilenfilter eingesetzt werden, um die Daten zu reduzieren, die auf dem Abonnenten erforderlich sind, ist diese Verarbeitung komplexer und kann langsamer ablaufen als die Veröffentlichung aller Zeilen in einer Tabelle. Wägen Sie die Vor- und Nachteile zwischen geringeren Speicherplatzanforderungen auf jedem Abonnenten und der Notwendigkeit eines maximalen Durchsatzes sorgfältig ab. Weitere Informationen zu Filtern finden Sie unter [veröffentlichten Filterdaten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
## Überlegungen zu Abonnements  
  
-   Verwenden Sie Pullabonnements, wenn sehr viele Abonnenten vorhanden sind.  
  
     Der Verteilungs-Agent oder der Merge-Agent wird auf dem Verteiler für Pushabonnements und auf dem Abonnenten für Pullabonnements ausgeführt. Die Verwendung von Pullabonnements kann die Leistung verbessern, indem Verarbeitungsvorgänge des Agents auf die Abonnenten verlagert werden. Weitere Informationen finden Sie unter [abonnieren Publikationen](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Initialisieren Sie gegebenenfalls das Abonnement erneut, wenn Abonnenten zu stark in Verzug geraten sind.  
  
     Wenn umfangreiche Änderungen an Abonnenten gesendet werden müssen, kann die Neuinitialisierung mit einer neuen Momentaufnahme schneller sein als das Verwenden der Replikation zum Verschieben der einzelnen Änderungen. Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
     Bei der Transaktionsreplikation zeigt der Replikationsmonitor auf der **nicht verteilte Befehle** Informationen zur Registerkarte: die Anzahl der Transaktionen in der Verteilungsdatenbank, die noch nicht an einen Abonnenten; und die geschätzte Zeit für das Verteilen dieser Transaktionen verteilt wurden. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Überlegungen zu Momentaufnahmen  
  
-   Führen Sie den Momentaufnahme-Agent nur bei Bedarf und außerhalb der Spitzenzeiten aus.  
  
     Der Momentaufnahme-Agent führt Massenkopieraktionen von Daten aus der veröffentlichten Tabelle auf dem Verleger in eine Datei im Momentaufnahmeordner auf dem Verteiler durch. Das Generieren einer Momentaufnahme kann die Ressourcen stark beanspruchen und sollte möglichst außerhalb der Spitzenzeiten stattfinden.  
  
-   Verwenden Sie eine Momentaufnahme im einheitlichen Modus, sofern keine Momentaufnahme im Zeichenmodus erforderlich ist.  
  
     Verwenden Sie die Standardmomentaufnahme im einheitlichen Modus für alle Abonnenten, ausgenommen Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Abonnenten und Abonnenten mit [!INCLUDE[ssEW](../../../includes/ssew-md.md)], die eine Momentaufnahme im Zeichenmodus erfordern.  
  
-   Verwenden Sie einen einzigen Momentaufnahmeordner für eine Veröffentlichung.  
  
     Beim Angeben der Veröffentlichungseigenschaften im Zusammenhang mit dem Momentaufnahmespeicherort stehen Optionen zur Auswahl, um Momentaufnahmedateien im Standardmomentaufnahmeordner, in einem alternativen Momentaufnahmeordner oder in beiden zu erstellen. Für das Erstellen von Momentaufnahmedateien in beiden Speicherorten ist beim Ausführen des Momentaufnahme-Agents zusätzlicher Datenträgerspeicher und Verarbeitungsaufwand erforderlich.  
  
-   Speichern Sie den Momentaufnahmeordner auf einem lokalen Laufwerk des Verteilers, das nicht zum Speichern von Datenbank- oder Protokolldateien verwendet wird.  
  
     Der Momentaufnahme-Agent führt einen sequenziellen Schreibvorgang für die Daten im Momentaufnahmeordner aus. Durch das Speichern des Momentaufnahmeordners auf einem Laufwerk, das nicht für Datenbank- oder Protokolldateien verwendet wird, werden Konflikte bezüglich des Datenträgerzugriffs reduziert, und der Momentaufnahmeprozess wird schneller ausgeführt.  
  
-   Wenn Sie die Abonnementdatenbank auf dem Abonnenten erstellen, sollten Sie das einfache oder das massenprotokollierte Wiederherstellungsmodell angeben. Dadurch werden die Masseneinfügungen während der Anwendung der Momentaufnahme auf dem Abonnenten nur in geringem Umfang protokolliert. Nachdem die Momentaufnahme auf die Abonnementdatenbank angewendet wurde, können Sie gegebenenfalls wieder zu einem anderen Wiederherstellungsmodell wechseln (replizierte Datenbanken unterstützen jedes Wiederherstellungsmodell). Weitere Informationen zum Auswählen eines Wiederherstellungsmodells finden Sie unter [& #40; wiederherstellen und Wiederherstellung (Übersicht) SQL Server & #41;](../../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
-   Verwenden Sie bei Netzwerken mit niedrigen Bandbreiten gegebenenfalls den alternativen Momentaufnahmeordner und komprimierte Momentaufnahmen auf Wechselmedien.  
  
     Das Komprimieren von Momentaufnahmedateien im alternativen Momentaufnahmeordner kann den Speicherplatzbedarf von Momentaufnahmen reduzieren und das Übertragen der Momentaufnahmedateien auf Wechselmedien vereinfachen.  
  
     Komprimierte Momentaufnahmen können in einigen Fällen die Leistung beim Übertragen der Momentaufnahmedateien im Netzwerk verbessern. Beim Komprimieren der Momentaufnahme fällt jedoch zusätzlicher Verarbeitungsaufwand für den Momentaufnahme-Agent an, wenn die Momentaufnahmedateien erstellt werden, sowie für den Verteilungs-Agent oder den Merge-Agent, wenn die Momentaufnahmedateien angewendet werden. Dies könnte das Erstellen von Momentaufnahmen verlangsamen und den Zeitaufwand für das Anwenden einer Momentaufnahme in manchen Fällen erhöhen. Darüber hinaus kann das Übertragen komprimierter Momentaufnahmen bei einem Netzwerkausfall nicht wieder aufgenommen werden, weshalb sie sich nicht für unzuverlässige Netzwerke eignen. Wägen Sie die Vor- und Nachteile sorgfältig ab, wenn Sie komprimierte Momentaufnahmen in einem Netzwerk verwenden. Weitere Informationen finden Sie unter [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md) und [Compressed Snapshots](../../../relational-databases/replication/compressed-snapshots.md).  
  
-   Initialisieren Sie ein Abonnement gegebenenfalls manuell.  
  
     In einigen Szenarien, wenn z. B. große Anfangsdatasets eine Rolle spielen, ist es vorteilhafter, ein Abonnement statt mit einer Momentaufnahme mit einer anderen Methode zu initialisieren. Weitere Informationen finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
## Agentparameter  
  
-   Reduzieren Sie die Meldungsstufen von Replikations-Agents, außer während erster Test-, Überwachungs- oder Debugverfahren.  
  
     Reduzieren der **– HistoryVerboseLevel** Parameter und die **– OutputVerboseLevel** Parameter des Verteilungs-Agents oder Merge-Agents. Dadurch wird die Anzahl der neuen Zeilen reduziert, die zum Nachverfolgen des Verlaufs und der Ausgabe von Agents eingefügt werden. Stattdessen werden frühere Verlaufsmeldungen mit dem gleichen Status auf die neuen Verlaufsinformationen aktualisiert. Erhöhen Sie die Meldungsstufen für das Testen, Überwachen und Debuggen, sodass Sie so viele Informationen zur Agent-Aktivität erhalten wie möglich.  
  
-   Verwenden der **– MaxBCPThreads** Parameter von der Snapshot-Agent, der Merge-Agent und der Verteiler-Agent (die Anzahl der angegebenen Threads sollte die Anzahl der Prozessoren auf dem Computer nicht überschreiten). Mit diesem Parameter wird die Anzahl der Massenkopiervorgänge angegeben, die beim Erstellen und Anwenden der Momentaufnahme parallel ausgeführt werden können.  
  
-   Verwenden der **– UseInprocLoader** -Parameter des Verteilungs-Agent und der Merge-Agent (dieser Parameter kann nicht verwendet werden, wenn veröffentlichte Tabellen XML-Spalten enthalten). Durch diesen Parameter verwendet der Agent beim Anwenden der Momentaufnahme den BULK INSERT-Befehl.  
  
 Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Anzeigen und Ändern von Replikations-Agent-Befehlszeilenparameter & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
-   [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
  