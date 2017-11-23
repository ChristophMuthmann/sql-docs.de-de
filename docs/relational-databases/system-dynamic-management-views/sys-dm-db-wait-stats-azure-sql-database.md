---
title: Sys. dm_db_wait_stats (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_wait_stats_TSQL
- dm_db_wait_stats
- sys.dm_db_wait_stats
- sys.dm_db_wait_stats_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_db_wait_stats dynamic management view
- dm_db_wait_stats
ms.assetid: 00abd0a5-bae0-4d71-b173-f7a14cddf795
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 465c768c9f5636463e4d124d224f9184ebc2dac8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbwaitstats-azure-sql-database"></a>sys.dm_db_wait_stats (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu allen Wartevorgängen in den Threads zurück, die während des Vorgangs ausgeführt wurden. In dieser aggregierten Sicht können Sie Leistungsprobleme bei [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] sowie bei bestimmten Abfragen und Batches diagnostizieren.  
  
 Bestimmte Arten von Wartezeiten während der Abfrageausführung können auf Engpässe oder Stillstände während der Abfrage hinweisen. Entsprechend können serverweite lange Wartezeiten oder hohe Wartevorgangsanzahlen auf Engpässe oder Hotspots im Zusammenhang mit Abfrageinteraktionen innerhalb der Serverinstanz hinweisen. So weisen beispielsweise Sperrenwartevorgänge auf Datenkonflikte durch Abfragen, Seiten-E/A-Latchwartevorgänge auf langsame E/A-Antwortzeiten und Seitenlatch-Updatewartevorgänge auf ein fehlerhaftes Dateilayout hin.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Name des Wartetyps. Weitere Informationen finden Sie unter [Wartetypen](#WaitTypes)weiter unten in diesem Thema.|  
|waiting_tasks_count|**bigint**|Anzahl von Wartevorgängen für diesen Wartetyp. Dieser Leistungsindikator wird beim Starten eines Wartevorgangs inkrementiert.|  
|wait_time_ms|**bigint**|Gesamtwartezeit für diesen Wartetyp (in Millisekunden). Diese Zeit beinhaltet signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Maximale Wartezeit für diesen Wartetyp.|  
|signal_wait_time_ms|**bigint**|Differenz zwischen dem Zeitpunkt der Signalisierung des wartenden Threads und dem Beginn der Ausführung.|  
  
## <a name="remarks"></a>Hinweise  
  
-   In dieser dynamischen Verwaltungssicht werden nur Daten für die aktuelle Datenbank angezeigt.  
  
-   Diese dynamische Verwaltungssicht zeigt die Zeit für abgeschlossene Wartevorgänge an. Aktuelle Wartevorgänge werden nicht angezeigt.  
  
-   Sobald eine Datenbank verschoben oder offline geschaltet wurde, werden die Leistungsindikatoren auf 0 (null) zurückgesetzt.  
  
-   Ein SQL Server-Arbeitsthread wird nicht als wartend eingestuft, wenn eine der folgenden Aussagen zutrifft:  
  
    -   Eine Ressource wird verfügbar.  
  
    -   Eine Warteschlange ist nicht leer.  
  
    -   Ein externer Prozess wird abgeschlossen.  
  
-   Diese Statistiken werden nicht über Failoverereignisse der SQL-Datenbank beibehalten. Alle Daten stellen einen Gesamtwert seit dem letzten Zurücksetzen der Statistiken dar.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung auf dem Server.  
  
##  <a name="WaitTypes"></a>Wartetypen  
 Ressourcenwartevorgänge  
 Ressourcenwartevorgänge finden dann statt, wenn ein Arbeitsthread den Zugriff auf eine Ressource anfordert, die nicht verfügbar ist, da sie von einem anderen Arbeitsthread verwendet wird oder noch nicht zur Verfügung steht. Beispiele für Ressourcenwartevorgänge sind Sperren, Latches, Netzwerk- und Datenträger-E/A-Wartevorgänge. Sperren und Latchwartevorgänge sind Vorgänge, die auf Synchronisierungsobjekte warten.  
  
 Warteschlangen-Wartevorgänge  
 Warteschlangen-Wartevorgänge finden statt, wenn sich ein Arbeitsthread im Leerlauf befindet und auf die Zuweisung von Arbeit wartet. Warteschlangen-Wartevorgänge treten am häufigsten bei Hintergrundtasks des Systems auf, wie z. B. der Deadlocküberwachung und dem Cleanup gelöschter Datensätze. Diese Tasks warten, dass Arbeitsanforderungen in einer Arbeitswarteschlange platziert werden. Warteschlangen-Wartevorgänge können in regelmäßigen Abständen selbst dann aktiviert werden, wenn keine neuen Pakete in die Warteschlange übertragen wurden.  
  
 Externe Wartevorgänge  
 Externe Wartevorgänge finden statt, wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arbeitsthread wartet darauf, dass ein externes Ereignis, z. B. eines erweiterten gespeicherten Prozeduraufrufs oder einer Verbindungsserverabfrage, um den Vorgang abzuschließen. Wenn Sie Probleme mit Blockierungen diagnostizieren, sollten Sie bedenken, dass externe Wartevorgänge nicht immer auf den Leerlauf eines Arbeitsthreads hinweisen, da der Arbeitsthread möglicherweise aktiv externen Code ausführt.  
  
 Obwohl der Thread nicht mehr wartet, muss er nicht sofort mit der Ausführung beginnen. Ein solcher Thread wird zunächst in die Warteschlange der ausführbaren Arbeitsthreads eingereiht und muss warten, dass ein Quantum auf dem Zeitplanungsmodul ausgeführt wird.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Wartezeit Leistungsindikatoren sind **"bigint"** Werte und daher nicht als fehleranfällig zum Rollover wie entsprechenden Leistungsindikatoren in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 In der folgenden Tabelle werden die Wartetypen für Tasks in einer Liste aufgeführt.  
  
|Wartetyp|Beschreibung|  
|---------------|-----------------|  
|ABR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|ASSEMBLY_LOAD|Tritt während des exklusiven Zugriffs auf das Laden einer Assembly auf.|  
|ASYNC_DISKPOOL_LOCK|Tritt beim Versuch auf, parallele Threads zu synchronisieren, die Tasks wie das Erstellen oder Initialisieren einer Datei ausführen.|  
|ASYNC_IO_COMPLETION|Tritt auf, wenn ein Task auf das Ende eines E/A-Vorgangs wartet.|  
|ASYNC_NETWORK_IO|Tritt bei Netzwerkschreibvorgängen auf, wenn der Task hinter dem Netzwerk blockiert ist. Überprüfen Sie, ob der Client Daten vom Server verarbeitet.|  
|AUDIT_GROUPCACHE_LOCK|Tritt bei einem Wartevorgang auf eine Sperre auf, die den Zugriff auf einen speziellen Cache steuert. Der Cache enthält Informationen zu den jeweiligen Überwachungen, mit denen die einzelnen Überwachungsaktionsgruppen überwacht werden sollen.|  
|AUDIT_LOGINCACHE_LOCK|Tritt bei einem Wartevorgang auf eine Sperre auf, die den Zugriff auf einen speziellen Cache steuert. Der Cache enthält Informationen zu den jeweiligen Überwachungen, die zum Überwachen der Überwachungsaktionsgruppen für die Anmeldung verwendet werden.|  
|AUDIT_ON_DEMAND_TARGET_LOCK|Tritt bei einem Wartevorgang auf eine Sperre auf, mit der eine einmalige Initialisierung überwachungsbezogener Ziele von erweiterten Ereignissen sichergestellt werden soll.|  
|AUDIT_XE_SESSION_MGR|Tritt bei einem Wartevorgang auf eine Sperre auf, mit der das Starten und Beenden überwachungsbezogener Ziele von erweiterten Ereignissen synchronisiert werden soll.|  
|BACKUP|Tritt auf, wenn ein Task im Rahmen der Sicherungsverarbeitung blockiert wird.|  
|BACKUP_OPERATOR|Tritt auf, wenn ein Task auf das Einlegen eines Bands wartet. Fragen Sie zum Anzeigen des Status des Bands [dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md). Wenn keine Bandeinlegung aussteht, kann dieser Wartetyp auf ein Hardwareproblem mit dem Bandlaufwerk hinweisen.|  
|BACKUPBUFFER|Tritt auf, wenn ein Sicherungstask auf Daten oder auf einen Puffer wartet, in dem Daten gespeichert werden sollen. Dies ist nur dann ein Standardwartetyp, wenn ein Task auf die Einlegung eines Bands wartet.|  
|BACKUPIO|Tritt auf, wenn ein Sicherungstask auf Daten oder auf einen Puffer wartet, in dem Daten gespeichert werden sollen. Dies ist nur dann ein Standardwartetyp, wenn ein Task auf die Einlegung eines Bands wartet.|  
|BACKUPTHREAD|Tritt auf, wenn ein Task auf das Ende eines Sicherungstasks wartet. Die Wartezeiten können lang sein (von einigen Minuten bis zu mehreren Stunden). Wenn der Task, auf den gewartet wird, Teil eines E/A-Prozesses ist, weist dieser Wartetyp nicht auf ein Problem hin.|  
|BAD_PAGE_PROCESS|Tritt auf, wenn die Hintergrundprotokollierung fehlerverdächtiger Seiten eine häufigere Ausführung als alle fünf Sekunden zu vermeiden versucht. Eine übermäßige Anzahl von fehlerverdächtigen Seiten bewirkt, dass die Protokollierung häufig ausgeführt wird.|  
|BROKER_CONNECTION_RECEIVE_TASK|Tritt auf, wenn auf einen Zugriff für den Empfang einer Nachricht an einem Verbindungsendpunkt gewartet wird. Der Empfangszugriff auf den Endpunkt wird serialisiert.|  
|BROKER_ENDPOINT_STATE_MUTEX|Tritt auf, wenn ein Konflikt über den Zugriff auf den Status eines Verbindungsendpunktes von [!INCLUDE[ssSB](../../includes/sssb-md.md)] vorliegt. Der Zugriff auf den Status für Änderungen wird serialisiert.|  
|BROKER_EVENTHANDLER|Tritt auf, wenn ein Task auf den primären Ereignishandler von wartet der [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Dieser Wartetyp sollte nur sehr kurz auftreten.|  
|BROKER_INIT|Tritt beim Initialisieren von [!INCLUDE[ssSB](../../includes/sssb-md.md)] in jeder aktiven Datenbank. Dieser Wartetyp sollte nicht häufig auftreten.|  
|BROKER_MASTERSTART|Tritt auf, wenn ein Task für den primären Ereignishandler von wartet die [!INCLUDE[ssSB](../../includes/sssb-md.md)] zu starten. Dieser Wartetyp sollte nur sehr kurz auftreten.|  
|BROKER_RECEIVE_WAITFOR|Tritt auf, wenn RECEIVE WAITFOR wartet. Dies ist ein Standardwartetyp, wenn keine Nachrichten empfangen werden können.|  
|BROKER_REGISTERALLENDPOINTS|Tritt auf, während der Initialisierung des eine [!INCLUDE[ssSB](../../includes/sssb-md.md)] Verbindungsendpunkt. Dieser Wartetyp sollte nur sehr kurz auftreten.|  
|BROKER_SERVICE|Tritt auf, wenn die einem Zieldienst zugeordnete [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Zielliste aktualisiert wird oder deren Priorität neu festgelegt wird.|  
|BROKER_SHUTDOWN|Tritt bei ein geplantes Herunterfahren von [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Dieser Wartetyp sollte, wenn überhaupt, nur sehr kurz auftreten.|  
|BROKER_TASK_STOP|Tritt auf, wenn die [!INCLUDE[ssSB](../../includes/sssb-md.md)] Warteschlangen-taskhandler auf den Task herunterzufahren. Die Statusüberprüfung wird serialisiert und muss vorher ausgeführt werden.|  
|BROKER_TO_FLUSH|Tritt auf, wenn die [!INCLUDE[ssSB](../../includes/sssb-md.md)] die speicherinternen Übertragungsobjekte in eine Arbeitstabelle lazy Arbeitstabelle geleert.|  
|BROKER_TRANSMITTER|Tritt auf, wenn die Übertragung von [!INCLUDE[ssSB](../../includes/sssb-md.md)] auf Arbeit wartet.|  
|BUILTIN_HASHKEY_MUTEX|Kann nach dem Start einer Instanz auftreten, während interne Datenstrukturen initialisiert werden. Tritt nach dem Initialisieren der Datenstrukturen nicht erneut auf.|  
|CHECK_PRINT_RECORD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|CHECKPOINT_QUEUE|Tritt auf, während der Prüfpunkttask auf die nächste Prüfpunktanforderung wartet.|  
|CHKPT|Tritt beim Starten des Servers auf, um dem Prüfpunktthread mitzuteilen, dass er beginnen kann.|  
|CLEAR_DB|Tritt während Vorgängen auf, die den Status einer Datenbank ändern, z. B. beim Öffnen oder Schließen einer Datenbank.|  
|CLR_AUTO_EVENT|Tritt bei der CLR (Common Language Runtime)-Ausführung eines Tasks auf, wenn dieser auf das Initialisieren eines bestimmten automatischen Ereignisses (autoevent) wartet. Lange Wartezeiten sind typisch und zeigen kein Problem an.|  
|CLR_CRST|Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf den Eintritt in einen kritischen Abschnitt des Tasks wartet, der zurzeit von einem anderen Task verwendet wird.|  
|CLR_JOIN|Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf das Ende eines anderen Tasks wartet. Dieser Wartestatus tritt auf, wenn ein Join zwischen Tasks besteht.|  
|CLR_MANUAL_EVENT|Tritt bei der CLR (Common Language Runtime)-Ausführung eines Tasks auf, wenn dieser auf das Initiieren eines bestimmten manuellen Ereignisses wartet.|  
|CLR_MEMORY_SPY|Tritt während eines Wartevorgangs auf den Erhalt einer Sperre für eine Datenstruktur auf, die zum Aufzeichnen aller virtuellen Speicherbelegungen aus der CLR verwendet wird. Die Datenstruktur wird gesperrt, um bei Parallelzugriffen die Integrität beizubehalten.|  
|CLR_MONITOR|Tritt bei der CLR (Common Language Runtime)-Ausführung eines Tasks auf, wenn dieser darauf wartet, eine Sperre für die Überwachung abrufen zu können.|  
|CLR_RWLOCK_READER|Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf eine Sperre des Lesers wartet.|  
|CLR_RWLOCK_WRITER|Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf eine Sperre des Schreibers wartet.|  
|CLR_SEMAPHORE|Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf eine Semaphore wartet.|  
|CLR_TASK_START|Tritt auf, während auf den Abschluss des Startvorgangs eines CLR-Tasks gewartet wird.|  
|CLRHOST_STATE_ACCESS|Tritt bei einem Wartevorgang auf den Erhalt von exklusivem Zugriff auf die CLR Hosting-Datenstrukturen auf. Dieser Wartetyp tritt auf, während die CLR-Laufzeit eingerichtet oder beendet wird.|  
|CMEMTHREAD|Tritt auf, wenn ein Task auf ein threadsicheres Speicherobjekt wartet. Die Wartezeit kann bei Konflikten zunehmen, die entstehen, wenn mehrere Tasks Speicher vom gleichen Speicherobjekt zuordnen.|  
|CXPACKET|Tritt beim Versuch auf, den Austauschiterator des Abfrageprozessors zu synchronisieren. Bei Problemen im Zusammenhang mit Konflikten für diesen Wartetyp kann es sinnvoll sein, den Grad der Parallelität zu senken.|  
|CXROWSET_SYNC|Tritt während eines parallelen Bereichsscans auf.|  
|DAC_INIT|Tritt während des Initialisierungsvorgangs der dedizierten Administratorverbindung auf.|  
|DBMIRROR_DBM_EVENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|DBMIRROR_DBM_MUTEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|DBMIRROR_EVENTS_QUEUE|Tritt auf, wenn die Datenbankspiegelung auf die Verarbeitung von Ereignissen wartet.|  
|DBMIRROR_SEND|Tritt auf, wenn ein Task auf die Beseitigung eines Kommunikationsrückstands auf der Netzwerkebene wartet, um Nachrichten senden zu können. Weist darauf hin, dass die Kommunikationsebene möglicherweise überlastet ist, was sich negativ auf den Datendurchsatz bei der Datenbankspiegelung auswirken kann.|  
|DBMIRROR_WORKER_QUEUE|Zeigt an, dass der Arbeitstask der Datenbankspiegelung auf weitere Arbeit wartet.|  
|DBMIRRORING_CMD|Tritt auf, wenn ein Task darauf wartet, dass Protokolldatensätze auf den Datenträger geleert werden. Dieser Wartestatus dauert erwartungsgemäß einige Zeit an.|  
|DEADLOCK_ENUM_MUTEX|Tritt auf, wenn die Deadlocküberwachung und sys.dm_os_waiting_tasks sicherstellen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehrere Deadlocksuchvorgänge gleichzeitig ausführt.|  
|DEADLOCK_TASK_SEARCH|Eine lange Wartezeit für diese Ressource zeigt an, dass der Server Abfragen zusätzlich zu sys.dm_os_waiting_tasks ausführt und diese Abfragen die Ausführung einer Deadlocksuche durch die Deadlocküberwachung blockieren. Dieser Wartetyp wird nur von der Deadlocküberwachung verwendet. Für Abfragen zusätzlich zu sys.dm_os_waiting_tasks wird DEADLOCK_ENUM_MUTEX verwendet.|  
|DEBUG|Tritt beim Debuggen von [!INCLUDE[tsql](../../includes/tsql-md.md)] und CLR für eine interne Synchronisierung auf.|  
|DISABLE_VERSIONING|Tritt auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fragt das Version-Transaktions-Manager, um festzustellen, ob der Zeitstempel der ältesten aktiven Transaktion als der Zeitstempel liegt des bei der Statuswechsel begonnen hat. Wenn dies der Fall ist, sind alle Momentaufnahmetransaktionen abgeschlossen, die vor dem Ausführen der ALTER DATABASE-Anweisung begonnen wurden. Dieser Wartestatus wird verwendet, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die versionsverwaltung mithilfe der ALTER DATABASE-Anweisung deaktiviert.|  
|DISKIO_SUSPEND|Tritt auf, wenn ein Task auf den Zugriff auf eine Datei wartet, wenn eine externe Sicherung aktiviert ist. Dieser Wartetyp wird für jeden wartenden Benutzerprozess gemeldet. Ein Wert über fünf pro Benutzerprozess kann darauf hinweisen, dass die externe Sicherung zu lange dauert.|  
|DISPATCHER_QUEUE_SEMAPHORE|Tritt auf, wenn ein Thread aus dem Verteilerpool auf weitere Arbeit wartet. Die Wartezeit für diesen Wartetyp steigt voraussichtlich, wenn der Verteiler im Leerlauf ist.|  
|DLL_LOADING_MUTEX|Tritt einmal auf, während auf das Laden der DLL des XML-Parsers gewartet wird.|  
|DROPTEMP|Tritt zwischen den Versuchen, ein temporäres Objekt zu löschen, auf, wenn beim vorherigen Versuch ein Fehler aufgetreten ist. Die Wartedauer nimmt mit jedem fehlerhaften Löschversuch exponentiell zu.|  
|DTC|Tritt auf, wenn ein Task auf ein Ereignis wartet, das für die Verwaltung des Statusübergangs verwendet wird. Dieser Status steuert, wann die Wiederherstellung [!INCLUDE[msCoName](../../includes/msconame-md.md)] Transaktionen Distributed Transaction Coordinator (MS DTC) tritt ein, nachdem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erhält eine Benachrichtigung, dass der MS DTC-Dienst nicht verfügbar ist.<br /><br /> Dieser Status beschreibt auch eine Aufgabe, die darauf, beim Initiieren eines Commits einer MS DTC-Transaktion warten durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] des MS DTC-Commits wartet.|  
|DTC_ABORT_REQUEST|Tritt in einer MS DTC-Arbeitsthreadsitzung auf, wenn die Sitzung darauf wartet, eine MS DTC-Transaktion in Besitz zu nehmen. Sobald MS DTC die Transaktion besitzt, kann die Sitzung ein Rollback der Transaktion ausführen. Im Allgemeinen wartet die Sitzung auf eine andere Sitzung, die die Transaktion verwendet.|  
|DTC_RESOLVE|Tritt auf, wenn ein Wiederherstellungstask auf die master-Datenbank in einer datenbankübergreifenden Transaktion wartet, damit der Task das Ergebnis der Transaktion abfragen kann.|  
|DTC_STATE|Tritt auf, wenn ein Task auf ein Ereignis wartet, das Änderungen am internen globalen Statusobjekt für MS DTC schützt. Dieser Status sollte nur sehr kurze Zeit andauern.|  
|DTC_TMDOWN_REQUEST|Tritt in einer MS DTC-Arbeitsthreadsitzung auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] benachrichtigt wird, dass der MS DTC-Dienst nicht zur Verfügung steht. Zunächst wartet der Arbeitsthread auf den Beginn des MS DTC-Wiederherstellungsprozesses. Dann wartet der Arbeitsthread darauf, das Ergebnis der verteilten Transaktion, an der der Arbeitsthread arbeitet, abrufen zu können. Dies kann so lange fortgesetzt werden, bis die Verbindung mit dem MS DTC-Dienst wiederhergestellt ist.|  
|DTC_WAITFOR_OUTCOME|Tritt auf, wenn Wiederherstellungstasks darauf warten, dass MS DTC aktiviert wird, damit vorbereitete Transaktionen aufgelöst werden können.|  
|DUMP_LOG_COORDINATOR|Tritt auf, wenn ein Haupttask darauf wartet, dass ein untergeordneter Task Daten generiert. Normalerweise tritt dieser Status nicht auf. Eine lange Wartezeit weist auf eine unerwartete Blockierung hin. In diesem Fall sollte der untergeordnete Task überprüft werden.|  
|DUMPTRIGGER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|EC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|EE_PMOLOCK|Tritt bei der Synchronisierung bestimmter Typen von Speicherbelegungen während der Ausführung von Anweisungen auf.|  
|EE_SPECPROC_MAP_INIT|Tritt bei der Synchronisierung der Erstellung der internen Prozedurhashtabelle auf. Dieser Wartevorgang kann nur beim ersten Zugriff auf die Hashtabelle nach dem Auftreten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz gestartet wird.|  
|ENABLE_VERSIONING|Tritt auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wartet aller Updatetransaktionen in dieser Datenbank abgeschlossen ist, bevor Sie deklarieren die Datenbank für den Übergang zum Status der Snapshot-Isolation bereit. Dieser Status wird verwendet, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Snapshot-Isolation mithilfe der ALTER DATABASE-Anweisung aktiviert.|  
|ERROR_REPORTING_MANAGER|Tritt bei der Synchronisierung mehrerer gleichzeitiger Fehlerprotokollinitialisierungen auf.|  
|EXCHANGE|Tritt während der Synchronisierung des Austauschiterators des Abfrageprozessors während paralleler Abfragen auf.|  
|EXECSYNC|Tritt während paralleler Abfragen bei der Synchronisierung im Abfrageprozessor in Bereichen auf, die nicht mit dem Austauschiterator verbunden sind. Beispiele für solche Bereiche sind Bitmaps, LOBs (Large Objects) und der Spooliterator. Dieser Wartestatus kann von LOBs häufig verwendet werden.|  
|EXECUTION_PIPE_EVENT_INTERNAL|Tritt während der Synchronisierung zwischen den Producer- und Consumerteilen der Batchausführung auf, die über den Verbindungskontext gesendet werden.|  
|FAILPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|FCB_REPLICA_READ|Tritt bei der Synchronisierung der Lesevorgänge einer Sparsedatei der Momentaufnahme (oder einer von DBCC erstellten temporären Momentaufnahme) auf.|  
|FCB_REPLICA_WRITE|Tritt beim Synchronisieren der Push- oder Pullvorgänge einer Seite in eine Sparsedatei der Momentaufnahme (oder einer von DBCC erstellten temporären Momentaufnahme) auf.|  
|FS_FC_RWLOCK|Tritt bei einem Wartevorgang auf die Durchführung einer der beiden folgenden Aktionen durch den FILESTREAM-Garbage Collector auf:<br /><br /> Deaktivieren der Garbage Collection (von Sicherung und Wiederherstellung verwendet)<br /><br /> Ausführen eines Zyklus des FILESTREAM-Garbage Collectors|  
|FS_GARBAGE_COLLECTOR_SHUTDOWN|Tritt auf, wenn der FILESTREAM-Garbage Collector auf das Abschließen von Cleanuptasks wartet.|  
|FS_HEADER_RWLOCK|Tritt bei einem Wartevorgang auf den Erhalt von Zugriff auf den FILESTREAM-Header eines FILESTREAM-Datencontainers auf, um entweder Inhalte in der FILESTREAM-Headerdatei (Filestream.hdr) zu lesen oder zu aktualisieren.|  
|FS_LOGTRUNC_RWLOCK|Tritt bei einem Wartevorgang auf den Erhalt von Zugriff auf die FILESTREAM-Protokollkürzung auf, um eine der beiden folgenden Aktionen auszuführen:<br /><br /> Vorübergehendes Deaktivieren der FILESTREAM (FSLOG)-Protokollkürzung (von Sicherung und Wiederherstellung verwendet)<br /><br /> Ausführen eines Zyklus der FSLOG-Kürzung|  
|FSA_FORCE_OWN_XACT|Tritt auf, wenn ein FILESTREAM-Datei-E/A-Vorgang an die zugeordnete Transaktion gebunden werden muss, die Transaktion jedoch gerade im Besitz einer anderen Sitzung ist.|  
|FSAGENT|Tritt auf, wenn ein FILESTREAM-Datei-E/A-Vorgang auf eine FILESTREAM-Agent-Ressource wartet, die gerade von einem anderen Datei-E/A-Vorgang verwendet wird.|  
|FSTR_CONFIG_MUTEX|Tritt bei einem Wartevorgang auf eine andere Neukonfiguration eines FILESTREAM-Funktionen auf, die abgeschlossen werden soll.|  
|FSTR_CONFIG_RWLOCK|Tritt bei einem Wartevorgang auf die Serialisierung des Zugriffs auf die FILESTREAM-Konfigurationsparameter auf.|  
|FT_METADATA_MUTEX|Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.|  
|FT_RESTART_CRAWL|Tritt auf, wenn ein Volltextcrawl von einem letzten bekannten fehlerfreien Punkt neu gestartet werden muss, um nach einem vorübergehenden Fehler wiederhergestellt zu werden. Durch die Wartezeit können die Arbeitstasks, die zurzeit an der jeweiligen Auffüllung arbeiten, abgeschlossen werden oder den aktuellen Schritt beenden.|  
|FULLTEXT GATHERER|Tritt bei der Synchronisierung von Volltextvorgängen auf.|  
|GUARDIAN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|HTTP_ENUMERATION|Tritt beim Starten auf, wenn die HTTP-Endpunkte zum Starten von HTTP aufgezählt werden sollen.|  
|HTTP_START|Tritt auf, wenn eine Verbindung auf den Abschluss der HTTP-Initialisierung wartet.|  
|IMPPROV_IOWAIT|Tritt auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wartet, bis eine Bulkload e/a, um den Vorgang abzuschließen.|  
|INTERNAL_TESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|IO_AUDIT_MUTEX|Tritt während der Synchronisierung von Ereignispuffern der Ablaufverfolgung auf.|  
|IO_COMPLETION|Tritt auf, während auf den Abschluss von E/A-Vorgängen gewartet wird. Dieser Wartetyp stellt in der Regel Nicht-Datenseiten-E/A-Vorgänge dar. E/A-Abschlusswartezeiten für Datenseiten werden als PAGEIOLATCH_*-Wartevorgänge angezeigt.|  
|IO_QUEUE_LIMIT|Tritt auf, wenn in der asynchronen E/A-Warteschlange für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] zu viele Lese- und Schreibvorgänge ausstehend sind. Aufgaben, die einen weiteren Lese-/Schreibvorgang initiieren, werden blockiert, bis die Anzahl der ausstehenden Lese-/Schreibvorgänge unter den Schwellenwert fällt Der Schwellenwert ist proportional zu den DTUs (Database Throughput Units), die der Datenbank zugewiesen sind.|  
|IO_RETRY|Tritt auf, wenn ein E/A-Vorgang, z. B. das Lesen von oder Schreiben auf einen Datenträger, aufgrund unzureichender Ressourcen scheitert und dann wiederholt wird.|  
|IOAFF_RANGE_QUEUE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KSOURCE_WAKEUP|Wird vom Dienststeuerungstask verwendet, während auf Anforderungen vom Dienstkontroll-Manager gewartet wird. Lange Wartezeiten werden erwartet und zeigen kein Problem an.|  
|KTM_ENLISTMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KTM_RECOVERY_MANAGER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KTM_RECOVERY_RESOLUTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LATCH_DT|Tritt beim Warten auf einen DT-Latch (Löschlatch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste von LATCH_*-Wartevorgängen ist in sys.dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.|  
|LATCH_EX|Tritt beim Warten auf einen EX-Latch (exklusiven Latch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste von LATCH_*-Wartevorgängen ist in sys.dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.|  
|LATCH_KP|Tritt beim Warten auf einen KP-Latch (Beibehaltungslatch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste von LATCH_*-Wartevorgängen ist in sys.dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.|  
|LATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LATCH_SH|Tritt beim Warten auf einen SH-Latch (gemeinsamen Latch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste von LATCH_*-Wartevorgängen ist in sys.dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.|  
|LATCH_UP|Tritt beim Warten auf einen UP-Latch (Updatelatch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste von LATCH_*-Wartevorgängen ist in sys.dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.|  
|LAZYWRITER_SLEEP|Tritt auf, wenn Tasks für verzögertes Schreiben angehalten werden. Dieser Wartetyp gibt die Zeitdauer von wartenden Hintergrundtasks an. Wenn Sie nach durch den Benutzer bedingtem Hängen des Computers suchen, sollten Sie diesen Status nicht verwenden.|  
|LCK_M_BU|Tritt auf, wenn ein Task darauf wartet, eine Massenupdatesperre (BU-Sperre) abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_IS|Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte gemeinsame Sperre (IS-Sperre) abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_IU|Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte Updatesperre (IU-Sperre) abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_IX|Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte exklusive Sperre (IX-Sperre) abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_NL|Tritt auf, wenn ein Task darauf wartet, eine NULL-Sperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Eine NULL-Sperre für den Schlüssel ist eine Sperre, die sofort aufgehoben wird. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_S|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_U|Ein Task wartet darauf, eine Updatesperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_X|Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RS_S|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre für den aktuellen Schlüsselwert und eine freigegebene Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RS_U|Tritt auf, wenn ein Task darauf wartet, eine Updatesperre für den aktuellen Schlüsselwert und eine Bereichsupdatesperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RX_S|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre für den aktuellen Schlüsselwert und eine exklusive Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RX_U|Tritt auf, wenn ein Task darauf wartet, eine Updatesperre für den aktuellen Schlüsselwert und eine exklusive Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RX_X|Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre für den aktuellen Schlüsselwert und eine exklusive Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_S|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SCH_M|Tritt auf, wenn ein Task darauf wartet, eine Schemaänderungssperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SCH_S|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Schemasperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SIU|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter Updatesperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SIX|Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter exklusiver Sperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_U|Tritt auf, wenn ein Task darauf wartet, eine Updatesperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_UIX|Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit beabsichtigter exklusiver Sperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_X|Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre abzurufen. Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LOG_RATE_GOVERNOR|Tritt auf, wenn die Datenbank auf ein Kontingent zum Schreiben des Protokolls wartet.|  
|LOGBUFFER|Tritt auf, wenn ein Task auf Speicherplatz im Protokollpuffer zum Speichern eines Protokolldatensatzes wartet. Durchgehend hohe Werte können darauf hinweisen, dass die Protokollgeräte die Menge der vom Server generierten Protokolldaten nicht bewältigen können.|  
|LOGGENERATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LOGMGR|Tritt auf, wenn ein Task beim Schließen der Datenbank vor dem Beenden des Protokolls auf das Fertigstellen ausstehender Protokoll-E/A-Vorgänge wartet.|  
|LOGMGR_FLUSH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LOGMGR_QUEUE|Tritt auf, während der Protokollschreibertask auf Arbeitsanforderungen wartet.|  
|LOGMGR_RESERVE_APPEND|Tritt auf, wenn ein Task darauf wartet, feststellen zu können, ob durch das Abschneiden von Protokollen Speicherplatz freigegeben wird, damit der Task einen neuen Protokolldatensatz schreiben kann. Erwägen Sie, die Größe der Protokolldatei(en) für die betroffene Datenbank zu erhöhen, um diese Wartezeit zu reduzieren.|  
|LOWFAIL_MEMMGR_QUEUE|Tritt auf, während darauf gewartet wird, dass Arbeitsspeicher zur Verwendung verfügbar ist.|  
|MSQL_DQ|Tritt auf, wenn ein Task auf das Ende eines verteilten Abfragevorgangs wartet. Dieser Wartetyp wird verwendet, um mögliche MARS-Anwendungsdeadlocks (Multiple Active Result Sets) zu erkennen. Die Wartezeit wird mit dem Ende des Aufrufs der verteilten Abfrage beendet.|  
|MSQL_XACT_MGR_MUTEX|Tritt auf, wenn ein Task darauf wartet, in den Besitz des Sitzungstransaktions-Managers zu gelangen, um einen Transaktionsvorgang auf Sitzungsebene auszuführen.|  
|MSQL_XACT_MUTEX|Tritt während der Synchronisierung der Transaktionsverwendung auf. Eine Anforderung muss den Mutex abrufen, bevor sie die Transaktion verwenden kann.|  
|MSQL_XP|Tritt auf, wenn ein Task auf das Ende einer erweiterten gespeicherten Prozedur wartet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet diesen Wartestatus, um mögliche MARS-Anwendungsdeadlocks zu erkennen. Die Wartezeit wird mit dem Ende des Aufrufs der erweiterten gespeicherten Prozedur beendet.|  
|MSSEARCH|Tritt während Aufrufen der Volltextsuche auf. Diese Wartezeit endet, wenn der Volltextvorgang abgeschlossen ist. Sie zeigt keinen Konflikt an, sondern die Dauer von Volltextvorgängen.|  
|NET_WAITFOR_PACKET|Tritt auf, wenn eine Verbindung während eines Netzwerklesevorgangs auf ein Netzwerkpaket wartet.|  
|OLEDB|Tritt auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client aufruft. Dieser Wartetyp wird nicht für die Synchronisierung verwendet. Er zeigt vielmehr die Dauer von Aufrufen des OLE DB-Anbieters an.|  
|ONDEMAND_TASK_QUEUE|Tritt auf, während ein Hintergrundtask auf Systemtaskanforderungen mit hoher Priorität wartet. Lange Wartezeiten zeigen an, dass keine Anforderungen mit hoher Priorität zu verarbeiten waren, und sollten kein Problem darstellen.|  
|PAGEIOLATCH_DT|Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Löschmodus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.|  
|PAGEIOLATCH_EX|Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im exklusiven Modus: Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.|  
|PAGEIOLATCH_KP|Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Beibehaltungsmodus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.|  
|PAGEIOLATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PAGEIOLATCH_SH|Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im freigegebenen Modus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.|  
|PAGEIOLATCH_UP|Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Updatemodus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.|  
|PAGELATCH_DT|Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Löschmodus.|  
|PAGELATCH_EX|Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im exklusiven Modus:|  
|PAGELATCH_KP|Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Beibehaltungsmodus.|  
|PAGELATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PAGELATCH_SH|Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im freigegebenen Modus.|  
|PAGELATCH_UP|Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Updatemodus.|  
|PARALLEL_BACKUP_QUEUE|Tritt beim Serialisieren der Ausgabe auf, die von RESTORE HEADERONLY, RESTORE FILELISTONLY oder RESTORE LABELONLY erstellt wurde.|  
|PREEMPTIVE_ABR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG|Tritt auf, wenn das Zeitplanungsmodul für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Betriebssystem (SQLOS) in den präemptiven Modus wechselt, um ein Überwachungsereignis in das Windows-Ereignisprotokoll zu schreiben.|  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG|Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein Überwachungsereignis in das Windows-Sicherheitsprotokoll zu schreiben.|  
|PREEMPTIVE_CLOSEBACKUPMEDIA|Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um Sicherungsmedien zu schließen.|  
|PREEMPTIVE_CLOSEBACKUPTAPE|Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein Bandsicherungsmedium zu schließen.|  
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE|Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein virtuelles Sicherungsmedium zu schließen.|  
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL|Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um Windows-Failoverclustervorgänge auszuführen.|  
|PREEMPTIVE_COM_COCREATEINSTANCE|Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein COM-Objekt zu erstellen.|  
|PREEMPTIVE_HADR_LEASE_MECHANISM|AlwaysOn-Verfügbarkeitsgruppen lease-Manager, die CSS-Diagnose plant.|  
|PREEMPTIVE_SOSTESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_STRESSDRIVER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_TESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_XETESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PRINT_ROLLBACK_PROGRESS|Wird verwendet, um zu warten, während Benutzerprozesse in einer Datenbank beendet werden, die mithilfe der ALTER DATABASE-Beendigungsklausel von einem Status in einen anderen versetzt wurde. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC|Tritt auf, wenn ein Hintergrundtask auf die Beendigung des Hintergrundtasks wartet, der (über Abruf) Windows Server-Failoverclusteringbenachrichtigungen empfängt.  Nur interne Verwendung.|  
|PWAIT_HADR_CLUSTER_INTEGRATION|Eine Append, ersetzungs- und/oder Löschvorgang wartet auf eine Schreibsperre in einer Always On-internen Liste (z. B. eine Liste von Netzwerken, Netzwerkadressen oder verfügbarkeitsgruppenlistenern).  Nur interne Verwendung.|  
|PWAIT_HADR_OFFLINE_COMPLETED|Eine AlwaysOn-Verfügbarkeit Gruppe Löschvorgang wartet darauf, dass die zielverfügbarkeitsgruppe offline geht, bevor Sie Windows Server Failover Clustering-Objekte zu zerstören.|  
|PWAIT_HADR_ONLINE_COMPLETED|Erstellen einer Always On oder Failovervorgang Verfügbarkeit wartet darauf, dass die zielverfügbarkeitsgruppe online geschaltet werden kann.|  
|PWAIT_HADR_POST_ONLINE_COMPLETED|Eine AlwaysOn-Verfügbarkeit Gruppe Löschvorgang wartet auf die Beendigung eines Hintergrundtasks, der als Teil eines vorherigen Befehls geplant wurde. Es darf z. B. einen Hintergrundtask geben, der Verfügbarkeitsdatenbanken an die primäre Rolle übergibt. Die DROP AVAILABILITY GROUP-DDL muss auf den Abschluss dieses Hintergrundtasks warten, um Racebedingungen zu verhindern.|  
|PWAIT_HADR_WORKITEM_COMPLETED|Interner Wartevorgang von einem Thread, der auf den Abschluss eines asynchronen Arbeitstasks wartet. Dies ist ein erwarteter Wartevorgang und wird in CSS verwendet.|  
|PWAIT_MD_LOGIN_STATS|Tritt während der internen Synchronisierung in Metadaten zu Anmeldestatistiken auf.|  
|PWAIT_MD_RELATION_CACHE|Tritt während der internen Synchronisierung in Metadaten zu Tabelle oder Index auf.|  
|PWAIT_MD_SERVER_CACHE|Tritt während der internen Synchronisierung in Metadaten zu Verbindungsservern auf.|  
|PWAIT_MD_UPGRADE_CONFIG|Tritt während der internen Synchronisierung beim Aktualisieren von serverweiten Konfigurationen auf.|  
|PWAIT_METADATA_LAZYCACHE_RWLOCk|Tritt während der internen Synchronisierung im Metadatencache zusammen mit einem durchlaufenden Index oder Statistiken in einer Tabelle auf.|  
|QPJOB_KILL|Weist darauf hin, dass das asynchrone automatische Update der Statistik durch den Aufruf von KILL beim Starten des Updates abgebrochen wurde. Der Abschlussthread wird angehalten, und es wird darauf gewartet, dass er mit dem Überwachen auf KILL-Befehle beginnt. Ein guter Wert liegt unter einer Sekunde.|  
|QPJOB_WAITFOR_ABORT|Weist darauf hin, dass das asynchrone automatische Update der Statistik durch den Aufruf von KILL während des Updates abgebrochen wurde. Das Update wurde jetzt beendet und wird so lange angehalten, bis die Nachrichtenkoordination des Abschlussthreads abgeschlossen ist. Dies ist ein gewöhnlicher, jedoch selten vorkommender Status, der sehr kurz sein sollte. Ein guter Wert liegt unter einer Sekunde.|  
|QRY_MEM_GRANT_INFO_MUTEX|Tritt auf, wenn die Arbeitsspeicherverwaltung für die Abfrageausführung den Zugriff auf statische Listen mit Informationen zu zugewiesenen Arbeitsspeichern steuert. Dieser Status listet Informationen zu den aktuellen zugewiesenen und wartenden Speicheranforderungen auf. Dieser Status ist ein einfacher Zugriffssteuerungsstatus. In diesem Status sollte es nie zu langen Wartezeiten kommen. Wird dieser Mutex nicht freigegeben, antworten alle neuen speicherbeanspruchenden Abfragen nicht mehr.|  
|QUERY_ERRHDL_SERVICE_DONE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN|Tritt in bestimmten Fällen auf, wenn eine Offlineindexerstellung parallel ausgeführt wird und die unterschiedlichen Arbeitsthreads, die die Sortierung ausführen, den Zugriff auf die Sortierungsdateien synchronisieren.|  
|QUERY_NOTIFICATION_MGR_MUTEX|Tritt während der Synchronisierung der Garbage Collection-Warteschlange im Abfragebenachrichtigungs-Manager auf.|  
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX|Tritt während der Statussynchronisierung für Transaktionen in Abfragebenachrichtigungen auf.|  
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX|Tritt während der internen Synchronisierung im Abfragebenachrichtigungs-Manager auf.|  
|QUERY_NOTIFICATION_UNITTEST_MUTEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_OPTIMIZER_PRINT_MUTEX|Tritt während der Synchronisierung der Erstellung der Diagnoseausgabe des Abfrageoptimierers auf. Dieser Wartetyp tritt nur auf, wenn diagnoseeinstellungen unter der Richtung des aktivierten [!INCLUDE[msCoName](../../includes/msconame-md.md)] Microsoft Support Services.|  
|QUERY_TRACEOUT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_WAIT_ERRHDL_SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|RECOVER_CHANGEDB|Tritt während der Synchronisierung des Datenbankstatus in einer Datenbank im betriebsbereiten Standbymodus auf.|  
|REPL_CACHE_ACCESS|Tritt während der Synchronisierung für einen Replikationsartikelcache auf. Während dieser Wartezeiten wird der Replikationsprotokollleser angehalten, und Anweisungen der Datendefinitionssprache (Data Definition Language, DDL) für eine veröffentlichte Tabelle werden blockiert.|  
|REPL_SCHEMA_ACCESS|Tritt während der Synchronisierung von Versionsinformationen des Replikationsschemas auf. Dieser Status ist vorhanden, wenn DDL-Anweisungen für das replizierte Objekt ausgeführt werden und wenn der Protokollleser ein versionsspezifisches Schema auf der Basis des Auftretens von DDL erstellt oder verwendet.|  
|REPLICA_WRITES|Tritt auf, während ein Task auf den Abschluss von Seitenschreibvorgängen in Datenbankmomentaufnahmen oder DBCC-Replikaten wartet.|  
|REQUEST_DISPENSER_PAUSE|Tritt auf, wenn ein Task auf den Abschluss aller ausstehenden E/A-Vorgänge wartet, damit E/A-Vorgänge in eine Datei für eine Momentaufnahmesicherung eingefroren werden können.|  
|REQUEST_FOR_DEADLOCK_SEARCH|Tritt auf, während die Deadlocküberwachung darauf wartet, die nächste Deadlocksuche zu starten. Dieser Wartetyp wird zwischen Deadlockerkennungen erwartet, und eine lange Gesamtwartezeit für diese Ressource zeigt kein Problem an.|  
|RESMGR_THROTTLED|Tritt auf, wenn eine neue Anforderung eingeht und auf der Basis der Einstellung GROUP_MAX_REQUESTS eingeschränkt wird.|  
|RESOURCE_QUEUE|Tritt während der Synchronisierung verschiedener interner Ressourcenwarteschlangen auf.|  
|RESOURCE_SEMAPHORE|Tritt auf, wenn einer Arbeitsspeicheranforderung einer Abfrage aufgrund von anderen gleichzeitigen Abfragen nicht sofort entsprochen werden kann. Lange Wartevorgänge und Wartezeiten zeigen möglicherweise eine überhöhte Anzahl gleichzeitiger Abfragen oder eine überhöhte Menge angeforderten Arbeitsspeichers an.|  
|RESOURCE_SEMAPHORE_MUTEX|Tritt auf, während eine Abfrage darauf wartet, dass ihre Anforderung einer Threadreservierung erfüllt wird. Der Wartetyp tritt außerdem beim Synchronisieren von Abfragekompilierungs- und Arbeitsspeicherzuweisungsanforderungen auf.|  
|RESOURCE_SEMAPHORE_QUERY_COMPILE|Tritt auf, wenn die Anzahl gleichzeitiger Abfragekompilierungen einen Drosselungsgrenzwert erreicht. Lange Wartevorgänge und Wartezeiten zeigen möglicherweise eine überhöhte Anzahl von Kompilierungen, Neukompilierungen oder nicht zwischenspeicherbaren Plänen an.|  
|RESOURCE_SEMAPHORE_SMALL_QUERY|Tritt auf, wenn einer Arbeitsspeicheranforderung einer kleinen Abfrage aufgrund von anderen gleichzeitigen Abfragen nicht sofort entsprochen werden kann. Die Wartezeit sollte wenige Sekunden nicht überschreiten, da der Server die Anforderung an den Hauptspeicherpool für Abfragen überträgt, wenn er den angeforderten Arbeitsspeicher nicht innerhalb weniger Sekunden erteilen kann. Lange Wartezeiten zeigen möglicherweise eine übermäßige Anzahl gleichzeitiger kleiner Abfragen bei gleichzeitiger Blockierung des Hauptspeicherpools durch wartende Abfragen an.|  
|SE_REPL_CATCHUP_THROTTLE|Tritt auf, wenn die Transaktion darauf wartet, dass die Verarbeitung eines der sekundären Datenbankreplikate voranschreitet.|  
|SE_REPL_COMMIT_ACK|Tritt auf, wenn die Transaktion darauf wartet, dass Quorumcommits von sekundären Replikaten bestätigt werden.|  
|SE_REPL_COMMIT_TURN|Tritt auf, wenn die Transaktion auf ein Commit wartet, nachdem Bestätigungen von Quorumcommits empfangen wurden.|  
|SE_REPL_ROLLBACK_ACK|Tritt auf, wenn die Transaktion darauf wartet, dass Quorumrollbacks von sekundären Replikaten bestätigt werden.|  
|SE_REPL_SLOW_SECONDARY_THROTTLE|Tritt auf, wenn der Thread auf eines der sekundären Datenbankreplikate wartet.|  
|SEC_DROP_TEMP_KEY|Tritt nach einem fehlerhaftem Versuch, einen temporären Sicherheitsschlüssel zu löschen, vor einem Wiederholungsversuch auf.|  
|SECURITY_MUTEX|Tritt bei einem Wartevorgang auf Mutexe auf, die den Zugriff auf die globale Liste von EKM (Extensible Key Management)-Kryptografieanbietern und die Sitzungsbereichsliste der EKM-Sitzungen steuern.|  
|SEQUENTIAL_GUID|Tritt auf, während eine neue sequenzielle GUID empfangen wird.|  
|SERVER_IDLE_CHECK|Tritt während der Synchronisierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz Leerlaufstatus auf, wenn ein Ressourcenmonitor versucht, Sie deklarieren eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz als im Leerlauf oder reaktivierungsversuch.|  
|SHUTDOWN|Tritt auf, während eine Anweisung zum Herunterfahren darauf wartet, dass aktive Verbindungen beendet werden.|  
|SLEEP_BPOOL_FLUSH|Tritt auf, wenn ein Prüfpunkt die Ausgabe neuer E/A-Vorgänge drosselt, um eine Überflutung des Datenträgersubsystems zu vermeiden.|  
|SLEEP_DBSTARTUP|Tritt beim Datenbankstart auf, während darauf gewartet wird, dass alle Datenbanken wiederhergestellt werden.|  
|SLEEP_DCOMSTARTUP|Tritt höchstens einmal beim Start einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz auf, während auf den Abschluss der DCOM-Initialisierung gewartet wird.|  
|SLEEP_MSDBSTARTUP|Tritt auf, wenn die SQL-Ablaufverfolgung auf den Abschluss des Startvorgangs der msdb-Datenbank wartet.|  
|SLEEP_SYSTEMTASK|Tritt beim Start eines Hintergrundtasks auf, während auf den Abschluss des Startvorgangs von tempdb gewartet wird.|  
|SLEEP_TASK|Tritt auf, wenn ein Task ruht, während auf das Auftreten eines generischen Ereignisses gewartet wird.|  
|SLEEP_TEMPDBSTARTUP|Tritt auf, während ein Task auf den Abschluss des Startvorgangs von tempdb wartet.|  
|SNI_CRITICAL_SECTION|Tritt während der internen Synchronisierung innerhalb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Netzwerkkomponenten.|  
|SNI_HTTP_WAITFOR_0_DISCON|Tritt während der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herunterfahren, während des Wartens auf ausstehender HTTP-Verbindungen beendet.|  
|SNI_LISTENER_ACCESS|Tritt auf, während darauf gewartet wird, dass nicht einheitliche Speicherzugriffsknoten (Non-Uniform Memory Access, NUMA) die Statusänderung aktualisieren. Der Zugriff auf die Statusänderung wird serialisiert.|  
|SNI_TASK_COMPLETION|Tritt bei einem Wartevorgang auf das Beenden aller Tasks während der Statusänderung eines NUMA-Knotens auf.|  
|SOAP_READ|Tritt während eines Wartevorgangs auf den Abschluss eines HTTP-Netzwerklesevorgangs auf.|  
|SOAP_WRITE|Tritt auf, während auf den Abschluss eines HTTP-Netzwerkschreibvorgangs gewartet wird.|  
|SOS_CALLBACK_REMOVAL|Tritt beim Ausführen einer Synchronisierung für eine Rückrufliste auf, um einen Rückruf zu entfernen. Es wird nicht erwartet, dass dieser Leistungsindikator nach dem Abschluss der Serverinitialisierung geändert wird.|  
|SOS_DISPATCHER_MUTEX|Tritt während der internen Synchronisierung des Verteilerpools auf. Dies schließt Anpassungsvorgänge des Pools mit ein.|  
|SOS_LOCALALLOCATORLIST|Tritt auf, während der internen Synchronisierung in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Speicher-Manager.|  
|SOS_MEMORY_USAGE_ADJUSTMENT|Tritt auf, wenn die Speicherauslastung zwischen Pools angepasst wird.|  
|SOS_OBJECT_STORE_DESTROY_MUTEX|Tritt während der internen Synchronisierung in Speicherpools auf, wenn Objekte im Pool gelöscht werden.|  
|SOS_PROCESS_AFFINITY_MUTEX|Tritt während der Synchronisierung des Zugriffs für die Verarbeitung von Affinitätseinstellungen auf.|  
|SOS_RESERVEDMEMBLOCKLIST|Tritt auf, während der internen Synchronisierung in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Speicher-Manager.|  
|SOS_SCHEDULER_YIELD|Tritt auf, wenn ein Task freiwillig das Zeitplanungsmodul freigibt, damit andere Tasks ausgeführt werden können. Während dieses Wartevorgangs wartet der Task darauf, dass sein Quantum erneuert wird.|  
|SOS_SMALL_PAGE_ALLOC|Tritt während der Zuordnung und Freigabe von Arbeitsspeicher auf, der von einigen Arbeitsspeicherobjekten verwaltet wird.|  
|SOS_STACKSTORE_INIT_MUTEX|Tritt während der Synchronisierung der Initialisierung des internen Speichers auf.|  
|SOS_SYNC_TASK_ENQUEUE_EVENT|Tritt auf, wenn ein Task synchron gestartet wird. Die meisten Tasks in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden asynchron gestartet. Dabei kehrt die Steuerung sofort zum Starter zurück, nachdem die Taskanforderung in der Arbeitswarteschlange angeordnet wurde.|  
|SOS_VIRTUALMEMORY_LOW|Tritt auf, wenn eine Speicherbelegung darauf wartet, dass ein Ressourcen-Manager virtuellen Arbeitsspeicher freigibt.|  
|SOSHOST_EVENT|Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf ein Ereignissynchronisierungsobjekt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wartet.|  
|SOSHOST_INTERNAL|Tritt während der Synchronisierung von Rückrufen des Speicher-Managers auf, die von gehosteten Komponenten, wie z. B. CLR, verwendet werden.|  
|SOSHOST_MUTEX|Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, wartet auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mutexsynchronisierungsobjekt.|  
|SOSHOST_RWLOCK|Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, wartet auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Leser-Synchronisierungsobjekt.|  
|SOSHOST_SEMAPHORE|Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf ein Semaphorensynchronisierungsobjekt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wartet.|  
|SOSHOST_SLEEP|Tritt auf, wenn ein gehosteter Task ruht, während auf das Auftreten eines generischen Ereignisses gewartet wird. Gehostete Tasks werden von gehosteten Komponenten, wie z. B. CLR, verwendet.|  
|SOSHOST_TRACELOCK|Tritt während der Synchronisierung des Zugriffs auf Ablaufverfolgungsdatenströme auf.|  
|SOSHOST_WAITFORDONE|Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf den Abschluss eines Tasks wartet.|  
|SQLCLR_APPDOMAIN|Tritt auf, während CLR auf den Abschluss des Startvorgangs einer Anwendungsdomäne wartet.|  
|SQLCLR_ASSEMBLY|Tritt auf, während auf den Zugriff auf die Liste der geladenen Assemblys in der Anwendungsdomäne gewartet wird.|  
|SQLCLR_DEADLOCK_DETECTION|Tritt auf, während CLR auf den Abschluss der Deadlockerkennung wartet.|  
|SQLCLR_QUANTUM_PUNISHMENT|Tritt auf, wenn ein CLR-Task gedrosselt wird, weil er sein Ausführungsquantum überschritten hat. Diese Drosselung wird ausgeführt, um die Auswirkungen dieses ressourcenintensiven Tasks auf andere Tasks zu reduzieren.|  
|SQLSORT_NORMMUTEX|Tritt bei der internen Synchronisierung auf, während interne Sortierungsstrukturen initialisiert werden.|  
|SQLSORT_SORTMUTEX|Tritt bei der internen Synchronisierung auf, während interne Sortierungsstrukturen initialisiert werden.|  
|SQLTRACE_BUFFER_FLUSH|Tritt auf, wenn ein Task darauf wartet, dass ein Hintergrundtask Ablaufverfolgungspuffer alle vier Sekunden auf den Datenträger leert.|  
|SQLTRACE_LOCK|Tritt während der Synchronisierung für Ablaufverfolgungspuffer während einer Dateiablaufverfolgung auf.|  
|SQLTRACE_SHUTDOWN|Tritt auf, während das Herunterfahren der Ablaufverfolgung auf den Abschluss ausstehender Ablaufverfolgungsereignisse wartet.|  
|SQLTRACE_WAIT_ENTRIES|Tritt auf, während eine Ereigniswarteschlange der SQL-Ablaufverfolgung auf das Eintreffen von Paketen in der Warteschlange wartet.|  
|SRVPROC_SHUTDOWN|Tritt auf, während der Prozess des Herunterfahrens auf die Freigabe interner Ressourcen wartet, damit ein ordnungsgemäßes Herunterfahren erfolgen kann.|  
|TEMPOBJ|Tritt auf, wenn Löschvorgänge temporärer Objekte synchronisiert werden. Dieser Wartetyp ist selten und tritt nur auf, wenn ein Task einen exklusiven Zugriff für temp-Tabellenlöschvorgänge angefordert hat.|  
|THREADPOOL|Tritt auf, wenn ein Task auf die weitere Ausführung eines Arbeitsthreads wartet. Dies kann anzeigen, dass die Einstellung für die maximale Anzahl von Arbeitsthreads zu niedrig ist oder die Ausführung von Batches ungewöhnlich lange dauert, wodurch die Anzahl der Arbeitsthreads reduziert wird, die für das Ausführen anderer Batches verfügbar sind.|  
|TIMEPRIV_TIMEPERIOD|Tritt während der internen Synchronisierung des Zeitgebers für erweiterte Ereignisse auf.|  
|TRACEWRITE|Tritt auf, wenn der Rowset-Ablaufverfolgungsanbieter der SQL-Ablaufverfolgung entweder auf einen freien Puffer oder auf einen Puffer mit zu verarbeitenden Ereignissen wartet.|  
|TRAN_MARKLATCH_DT|Tritt auf, wenn auf einen Latch im Löschmodus für einen Transaktionsmarkierungslatch gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.|  
|TRAN_MARKLATCH_EX|Tritt auf, wenn auf einen Latch im exklusiven Modus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.|  
|TRAN_MARKLATCH_KP|Tritt auf, wenn auf einen Latch im Beibehaltungsmodus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.|  
|TRAN_MARKLATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|TRAN_MARKLATCH_SH|Tritt auf, wenn auf einen Latch im freigegebenen Modus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.|  
|TRAN_MARKLATCH_UP|Tritt auf, wenn auf einen Latch im Updatemodus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.|  
|TRANSACTION_MUTEX|Tritt während der Synchronisierung des Zugriffs auf eine Transaktion durch mehrere Batches auf.|  
|UTIL_PAGE_ALLOC|Tritt auf, wenn Transaktionsprotokollscans darauf warten, dass Arbeitsspeicher bei unzureichendem Arbeitsspeicher verfügbar ist.|  
|VIA_ACCEPT|Tritt auf, wenn eine VIA (Virtual Interface Adapter)-Anbieterverbindung während des Startvorgangs abgeschlossen wird.|  
|VIEW_DEFINITION_MUTEX|Tritt während der Synchronisierung für den Zugriff auf zwischengespeicherte Sichtdefinitionen auf.|  
|WAIT_FOR_RESULTS|Tritt auf, wenn auf das Auslösen einer Abfragebenachrichtigung gewartet wird.|  
|WAITFOR|Tritt als Ergebnis der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung WAITFOR auf. Die Dauer des Wartevorgangs wird durch die Parameter der Anweisung bestimmt. Hierbei handelt es sich um einen vom Benutzer initiierten Wartevorgang.|  
|WAITFOR_TASKSHUTDOWN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|WAITSTAT_MUTEX|Tritt während der Synchronisierung des Zugriffs auf die Statistikauflistung auf, die zum Auffüllen von sys.dm_os_wait_stats verwendet wird.|  
|WCC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|WORKTBL_DROP|Tritt während des Anhaltens vor einem erneuten Versuch nach einem fehlerhaften Löschvorgang einer Arbeitstabelle auf.|  
|WRITE_COMPLETION|Tritt während der Ausführung eines Schreibvorgangs auf.|  
|WRITELOG|Tritt auf, während auf den Abschluss einer Protokollleerung gewartet wird. Häufig verwendete Vorgänge, die Protokollleerungen verursachen, sind Prüfpunkte und Transaktionscommits.|  
|XACT_OWN_TRANSACTION|Tritt auf, während auf das Abrufen des Besitzes einer Transaktion gewartet wird.|  
|XACT_RECLAIM_SESSION|Tritt auf, während darauf gewartet wird, dass der aktuelle Besitzer einer Sitzung den Besitz der Sitzung freigibt.|  
|XACTLOCKINFO|Tritt während der Synchronisierung des Zugriffs auf die Liste von Sperren für eine Transaktion auf. Zusätzlich zur Transaktion selbst erfolgt der Zugriff auf die Liste von Sperren durch Vorgänge, wie z. B. Deadlockerkennung und Sperrenmigration, während Seitenteilungen.|  
|XACTWORKSPACE_MUTEX|Tritt während der Synchronisierung von Austritten aus einer Transaktion sowie der Anzahl von Datenbanksperren zwischen eingetragenen Mitgliedern einer Transaktion auf.|  
|XE_BUFFERMGR_ALLPROCESSED_EVENT|Tritt auf, wenn Puffer einer Sitzung für erweiterte Ereignisse an Ziele gesendet werden. Dieser Wartetyp tritt in einem Hintergrundthread auf.|  
|XE_BUFFERMGR_FREEBUF_EVENT|Tritt auf, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> Eine Sitzung für erweiterte Ereignisse ist so konfiguriert, dass Ereignisverluste nicht zulässig sind, und alle Puffer in der Sitzung sind gegenwärtig voll. Dies kann bedeuten, dass die Puffer einer Sitzung für erweiterte Ereignisse zu klein sind oder dass sie partitioniert werden sollten.<br /><br /> Während Überwachungen erfolgt eine Verzögerung. Dies kann bedeuten, dass auf dem Laufwerk, auf das die Überwachungen geschrieben werden, ein Datenträgerengpass vorhanden ist.|  
|XE_DISPATCHER_CONFIG_SESSION_LIST|Tritt auf, wenn eine Sitzung für erweiterte Ereignisse, die asynchrone Ziele verwendet, begonnen oder beendet wird. Dieser Wartetyp weist auf eines der folgenden Ereignisse hin:<br /><br /> Eine Sitzung für erweiterte Ereignisse wird bei einem Hintergrundthreadpool registriert.<br /><br /> Der Hintergrundthreadpool berechnet die erforderliche Anzahl von Threads anhand der aktuellen Last.|  
|XE_DISPATCHER_JOIN|Tritt auf, wenn ein für Sitzungen für erweiterte Ereignisse verwendeter Hintergrundthread beendet wird.|  
|XE_DISPATCHER_WAIT|Tritt auf, wenn ein für Sitzungen für erweiterte Ereignisse verwendeter Hintergrundthread auf die Verarbeitung von Ereignispuffern wartet.|  
|XE_MODULEMGR_SYNC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|XE_OLS_LOCK|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|XE_PACKAGE_LOCK_BACKOFF|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|FT_COMPROWSET_RWLOCK|Volltext wartet auf Metadatenvorgang für Fragment. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.|  
|FT_IFTS_RWLOCK|Volltext wartet auf interne Synchronisierung. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.|  
|FT_IFTS_SCHEDULER_IDLE_WAIT|Volltext-Wartetyp für den Ruhezustand des Zeitplanungsmoduls. Das Zeitplanungsmodul befindet sich im Leerlauf.|  
|FT_IFTSHC_MUTEX|Volltext wartet auf einen fdhost-Steuerungsvorgang. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.|  
|FT_IFTSISM_MUTEX|Volltext wartet auf einen Kommunikationsvorgang. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.|  
|FT_MASTER_MERGE|Volltext wartet auf Masterzusammenführungsvorgang. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.|  
  
  
