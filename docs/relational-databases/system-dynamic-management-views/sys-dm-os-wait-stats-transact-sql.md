---
title: Sys. dm_os_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: 111
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 55eaa65cc99bdc2e25e860be65570be6c8e32bdd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt Informationen zu allen Wartevorgängen in den Threads zurück, die ausgeführt wurden. In dieser aggregierten Sicht können Sie Leistungsprobleme bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sowie bei bestimmten Abfragen und Batches diagnostizieren. [Sys. dm_exec_session_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) enthält ähnliche Informationen von der Sitzung.  
  
> [!NOTE] 
> Aufrufen von **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**, verwenden Sie den Namen **sys.dm_pdw_nodes_os_wait_stats**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Name des Wartetyps. Weitere Informationen finden Sie unter [Wartetypen](#WaitTypes)weiter unten in diesem Thema.|  
|waiting_tasks_count|**bigint**|Anzahl von Wartevorgängen für diesen Wartetyp. Dieser Leistungsindikator wird beim Starten eines Wartevorgangs inkrementiert.|  
|wait_time_ms|**bigint**|Gesamtwartezeit für diesen Wartetyp (in Millisekunden). Diese Zeit beinhaltet signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Maximale Wartezeit für diesen Wartetyp.|  
|signal_wait_time_ms|**bigint**|Differenz zwischen dem Zeitpunkt der Signalisierung des wartenden Threads und dem Beginn der Ausführung.|  
|pdw_node_id|**int**|Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet. <br/> **Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

##  <a name="WaitTypes"></a> Wartetypen  
 **Ressourcenwartevorgänge** ressourcenwartevorgänge auftreten, wenn ein Arbeitsthread den Zugriff auf eine Ressource, die nicht verfügbar ist anfordert, da Sie von einem anderen Arbeitsthread verwendet wird oder ist noch nicht verfügbar. Beispiele für Ressourcenwartevorgänge sind Sperren, Latches, Netzwerk- und Datenträger-E/A-Wartevorgänge. Sperren und Latchwartevorgänge sind Vorgänge, die auf Synchronisierungsobjekte warten.  
  
**Warteschlangen-Wartevorgänge**  
 Warteschlangen-Wartevorgänge finden statt, wenn sich ein Arbeitsthread im Leerlauf befindet und auf die Zuweisung von Arbeit wartet. Warteschlangen-Wartevorgänge treten am häufigsten bei Hintergrundtasks des Systems auf, wie z. B. der Deadlocküberwachung und dem Cleanup gelöschter Datensätze. Diese Tasks warten, dass Arbeitsanforderungen in einer Arbeitswarteschlange platziert werden. Warteschlangen-Wartevorgänge können in regelmäßigen Abständen selbst dann aktiviert werden, wenn keine neuen Pakete in die Warteschlange übertragen wurden.  
  
 **Externe Wartevorgänge**  
 Externe Wartevorgänge finden statt, wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arbeitsthread wartet darauf, dass ein externes Ereignis, z. B. eines erweiterten gespeicherten Prozeduraufrufs oder einer Verbindungsserverabfrage, um den Vorgang abzuschließen. Wenn Sie Probleme mit Blockierungen diagnostizieren, sollten Sie bedenken, dass externe Wartevorgänge nicht immer auf den Leerlauf eines Arbeitsthreads hinweisen, da der Arbeitsthread möglicherweise aktiv externen Code ausführt.  
  
 `sys.dm_os_wait_stats` zeigt die Zeit für abgeschlossene Wartevorgänge an. Aktuelle Wartevorgänge werden in dieser dynamischen Verwaltungssicht nicht angezeigt.  
  
 Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Arbeitsthread wird nicht als wartend eingestuft, wenn eine der folgenden Aussagen zutrifft:  
  
-   Eine Ressource wird verfügbar.  
  
-   Eine Warteschlange ist nicht leer.  
  
-   Ein externer Prozess wird abgeschlossen.  
  
 Obwohl der Thread nicht mehr wartet, muss er nicht sofort mit der Ausführung beginnen. Ein solcher Thread wird zunächst in die Warteschlange der ausführbaren Arbeitsthreads eingereiht und muss warten, dass ein Quantum auf dem Zeitplanungsmodul ausgeführt wird.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Wartezeit Leistungsindikatoren sind **"bigint"** Werte und daher nicht als fehleranfällig zum Rollover wie entsprechenden Leistungsindikatoren in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Bestimmte Arten von Wartezeiten während der Abfrageausführung können auf Engpässe oder Stillstände während der Abfrage hinweisen. Entsprechend können serverweite lange Wartezeiten oder hohe Wartevorgangsanzahlen auf Engpässe oder Hotspots im Zusammenhang mit Abfrageinteraktionen innerhalb der Serverinstanz hinweisen. So weisen beispielsweise Sperrenwartevorgänge auf Datenkonflikte durch Abfragen, Seiten-E/A-Latchwartevorgänge auf langsame E/A-Antwortzeiten und Seitenlatch-Updatewartevorgänge auf ein fehlerhaftes Dateilayout hin.  
  
 Der Inhalt dieser dynamischen Verwaltungssicht kann durch Ausführen des folgenden Befehls zurückgesetzt werden:  
  
```sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
Dieser Befehl setzt alle Leistungsindikatoren auf 0 zurück.  
  
> [!NOTE]
> Diese Statistiken sind bei einem Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht permanent. Alle Daten stellen einen Gesamtwert seit dem letzten Zurücksetzen der Statistiken oder dem Neustarten des Servers dar.  
  
 In der folgenden Tabelle werden die Wartetypen für Tasks in einer Liste aufgeführt.  

|Typ |Description| 
|-------------------------- |--------------------------| 
|ABR |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_LOAD |Tritt während des exklusiven Zugriffs auf das Laden einer Assembly auf.| 
|ASYNC_DISKPOOL_LOCK |Tritt beim Versuch auf, parallele Threads zu synchronisieren, die Tasks wie das Erstellen oder Initialisieren einer Datei ausführen.| 
|ASYNC_IO_COMPLETION |Tritt auf, wenn ein Task auf das Ende eines E/A-Vorgangs wartet.| 
|ASYNC_NETWORK_IO |Tritt bei Netzwerkschreibvorgängen auf, wenn der Task hinter dem Netzwerk blockiert ist. Überprüfen Sie, ob der Client Daten vom Server verarbeitet.| 
|ASYNC_OP_COMPLETION |TBD <br />**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_SOCKETDUP_IO |TBD <br />**Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AUDIT_GROUPCACHE_LOCK |Tritt bei einem Wartevorgang auf eine Sperre auf, die den Zugriff auf einen speziellen Cache steuert. Der Cache enthält Informationen zu den jeweiligen Überwachungen, mit denen die einzelnen Überwachungsaktionsgruppen überwacht werden sollen.| 
|AUDIT_LOGINCACHE_LOCK |Tritt bei einem Wartevorgang auf eine Sperre auf, die den Zugriff auf einen speziellen Cache steuert. Der Cache enthält Informationen zu den jeweiligen Überwachungen, die zum Überwachen der Überwachungsaktionsgruppen für die Anmeldung verwendet werden.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |Tritt bei einem Wartevorgang auf eine Sperre auf, mit der eine einmalige Initialisierung überwachungsbezogener Ziele von erweiterten Ereignissen sichergestellt werden soll.| 
|AUDIT_XE_SESSION_MGR |Tritt bei einem Wartevorgang auf eine Sperre auf, mit der das Starten und Beenden überwachungsbezogener Ziele von erweiterten Ereignissen synchronisiert werden soll.| 
|BACKUP |Tritt auf, wenn ein Task im Rahmen der Sicherungsverarbeitung blockiert wird.| 
|BACKUP_OPERATOR |Tritt auf, wenn ein Task auf das Einlegen eines Bands wartet. Fragen Sie zum Anzeigen des Status des Bands dm_io_backup_tapes. Wenn keine Bandeinlegung aussteht, kann dieser Wartetyp auf ein Hardwareproblem mit dem Bandlaufwerk hinweisen.| 
|BACKUPBUFFER |Tritt auf, wenn ein Sicherungstask auf Daten oder auf einen Puffer wartet, in dem Daten gespeichert werden sollen. Dies ist nur dann ein Standardwartetyp, wenn ein Task auf die Einlegung eines Bands wartet.| 
|BACKUPIO |Tritt auf, wenn ein Sicherungstask auf Daten oder auf einen Puffer wartet, in dem Daten gespeichert werden sollen. Dies ist nur dann ein Standardwartetyp, wenn ein Task auf die Einlegung eines Bands wartet.| 
|BACKUPTHREAD |Tritt auf, wenn ein Task auf das Ende eines Sicherungstasks wartet. Die Wartezeiten können lang sein (von einigen Minuten bis zu mehreren Stunden). Wenn der Task, auf den gewartet wird, Teil eines E/A-Prozesses ist, weist dieser Wartetyp nicht auf ein Problem hin.| 
|BAD_PAGE_PROCESS |Tritt auf, wenn die Hintergrundprotokollierung fehlerverdächtiger Seiten eine häufigere Ausführung als alle fünf Sekunden zu vermeiden versucht. Eine übermäßige Anzahl von fehlerverdächtigen Seiten bewirkt, dass die Protokollierung häufig ausgeführt wird.| 
|BLOB_METADATA |TBD <br />**Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPALLOCATION |TBD <br />**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPBUILD |TBD <br />**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPARTITION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPLICATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BPSORT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_CONNECTION_RECEIVE_TASK |Tritt auf, wenn auf einen Zugriff für den Empfang einer Nachricht an einem Verbindungsendpunkt gewartet wird. Der Empfangszugriff auf den Endpunkt wird serialisiert.| 
|BROKER_DISPATCHER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_ENDPOINT_STATE_MUTEX |Tritt auf, wenn ein Systemressourcenkonflikt auftritt Zugriff auf den Status des Endpunkts einer Service Broker-Verbindung. Der Zugriff auf den Status für Änderungen wird serialisiert.| 
|BROKER_EVENTHANDLER |Tritt auf, wenn ein Task auf den primären Ereignishandler von Service Broker wartet. Dieser Wartetyp sollte nur sehr kurz auftreten.| 
|BROKER_FORWARDER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_INIT |Tritt auf, wenn Service Broker in jeder aktiven Datenbank zu initialisieren. Dieser Wartetyp sollte nicht häufig auftreten.| 
|BROKER_MASTERSTART |Tritt auf, wenn ein Task der primäre Ereignishandler von Service Broker wartet zu starten. Dieser Wartetyp sollte nur sehr kurz auftreten.| 
|BROKER_RECEIVE_WAITFOR |Tritt auf, wenn RECEIVE WAITFOR wartet. Dies kann bedeuten, dass keine Nachrichten in der Warteschlange empfangen werden können, oder ein Konflikt bei Sperre verhindert, dass er Nachrichten aus der Warteschlange empfangen.| 
|BROKER_REGISTERALLENDPOINTS |Tritt auf, während der Initialisierung des Service Broker-Endpunkt-Verbindung. Dieser Wartetyp sollte nur sehr kurz auftreten.| 
|BROKER_SERVICE |Tritt auf, wenn die Liste der Service Broker-Ziel, die einen Zieldienst zugeordnet ist, aktualisiert oder erneut priorisiert wird.| 
|BROKER_SHUTDOWN |Tritt bei ein geplantes Herunterfahren von Service Broker. Dieser Wartetyp sollte, wenn überhaupt, nur sehr kurz auftreten.| 
|BROKER_START |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_STOP |Tritt auf, wenn die Service Broker-Warteschlange taskhandler, den Task herunterzufahren. Die Statusüberprüfung wird serialisiert und muss vorher ausgeführt werden.| 
|BROKER_TASK_SUBMIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TO_FLUSH |Tritt auf, wenn die Service Broker lazy flusher Leerungen im Arbeitsspeicher Übertragung in eine Arbeitstabelle Objekte.| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMITTER |Tritt auf, wenn Service Broker-Übermittler auf Arbeit wartet.| 
|BUILTIN_HASHKEY_MUTEX |Kann nach dem Start einer Instanz auftreten, während interne Datenstrukturen initialisiert werden. Tritt nach dem Initialisieren der Datenstrukturen nicht erneut auf.| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_PRINT_RECORD |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|CHECK_SCANNER_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECKPOINT_QUEUE |Tritt auf, während der Prüfpunkttask auf die nächste Prüfpunktanforderung wartet.| 
|CHKPT |Tritt beim Starten des Servers auf, um dem Prüfpunktthread mitzuteilen, dass er beginnen kann.| 
|CLEAR_DB |Tritt während Vorgängen auf, die den Status einer Datenbank ändern, z. B. beim Öffnen oder Schließen einer Datenbank.| 
|CLR_AUTO_EVENT |Tritt bei der CLR (Common Language Runtime)-Ausführung eines Tasks auf, wenn dieser auf das Initialisieren eines bestimmten automatischen Ereignisses (autoevent) wartet. Lange Wartezeiten sind typisch und zeigen kein Problem an.| 
|CLR_CRST |Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf den Eintritt in einen kritischen Abschnitt des Tasks wartet, der zurzeit von einem anderen Task verwendet wird.| 
|CLR_JOIN |Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf das Ende eines anderen Tasks wartet. Dieser Wartestatus tritt auf, wenn ein Join zwischen Tasks besteht.| 
|CLR_MANUAL_EVENT |Tritt bei der CLR (Common Language Runtime)-Ausführung eines Tasks auf, wenn dieser auf das Initiieren eines bestimmten manuellen Ereignisses wartet.| 
|CLR_MEMORY_SPY |Tritt während eines Wartevorgangs auf den Erhalt einer Sperre für eine Datenstruktur auf, die zum Aufzeichnen aller virtuellen Speicherbelegungen aus der CLR verwendet wird. Die Datenstruktur wird gesperrt, um bei Parallelzugriffen die Integrität beizubehalten.| 
|CLR_MONITOR |Tritt bei der CLR (Common Language Runtime)-Ausführung eines Tasks auf, wenn dieser darauf wartet, eine Sperre für die Überwachung abrufen zu können.| 
|CLR_RWLOCK_READER |Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf eine Sperre des Lesers wartet.| 
|CLR_RWLOCK_WRITER |Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf eine Sperre des Schreibers wartet.| 
|CLR_SEMAPHORE |Tritt bei der CLR-Ausführung (Common Language Runtime) eines Tasks auf, wenn dieser auf eine Semaphore wartet.| 
|CLR_TASK_START |Tritt auf, während auf den Abschluss des Startvorgangs eines CLR-Tasks gewartet wird.| 
|CLRHOST_STATE_ACCESS |Tritt bei einem Wartevorgang auf den Erhalt von exklusivem Zugriff auf die CLR Hosting-Datenstrukturen auf. Dieser Wartetyp tritt auf, während die CLR-Laufzeit eingerichtet oder beendet wird.| 
|CMEMPARTITIONED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CMEMTHREAD |Tritt auf, wenn ein Task auf ein threadsicheres Speicherobjekt wartet. Die Wartezeit kann bei Konflikten zunehmen, die entstehen, wenn mehrere Tasks Speicher vom gleichen Speicherobjekt zuordnen.| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COUNTRECOVERYMGR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CREATE_DATINISERVICE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CXCONSUMER |Tritt bei parallelen Abfrageplänen, wenn ein Consumerthread wartet, einen Producerthread Zeilen zu senden. Dies ist ein normaler Bestandteil parallele abfrageausführung. <br /> **Gilt für**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 und [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |Tritt bei parallelen Abfrageplänen auf, wenn es sich bei den austauschiterator des Abfrageprozessors zu synchronisieren, und erzeugen und Nutzen von Zeilen. Wenn die Wartezeit zu lang ist und durch eine Abfrageoptimierung (beispielsweise durch das Hinzufügen von Indizes) nicht verkürzt werden kann, sollten Sie erwägen, den Kostenschwellenwert für Parallelität anzupassen oder den Grad an Parallelität zu verringern.<br /> **Hinweis:** In [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 und [!INCLUDE[ssSDS](../../includes/sssds-md.md)], CXPACKET nur verweist, den austauschiterator des Abfrageprozessors zu synchronisieren, und Zeilen für Consumer Threads erzeugen. Consumer-Threads werden in der Wartetyp CXCONSUMER separat nachverfolgt.| 
|CXROWSET_SYNC |Tritt während eines parallelen Bereichsscans auf.| 
|DAC_INIT |Tritt während des Initialisierungsvorgangs der dedizierten Administratorverbindung auf.| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBMIRROR_DBM_EVENT |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|DBMIRROR_DBM_MUTEX |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|DBMIRROR_EVENTS_QUEUE |Tritt auf, wenn die Datenbankspiegelung auf die Verarbeitung von Ereignissen wartet.| 
|DBMIRROR_SEND |Tritt auf, wenn ein Task auf die Beseitigung eines Kommunikationsrückstands auf der Netzwerkebene wartet, um Nachrichten senden zu können. Weist darauf hin, dass die Kommunikationsebene möglicherweise überlastet ist, was sich negativ auf den Datendurchsatz bei der Datenbankspiegelung auswirken kann.| 
|DBMIRROR_WORKER_QUEUE |Zeigt an, dass der Arbeitstask der Datenbankspiegelung auf weitere Arbeit wartet.| 
|DBMIRRORING_CMD |Tritt auf, wenn ein Task darauf wartet, dass Protokolldatensätze auf den Datenträger geleert werden. Dieser Wartestatus dauert erwartungsgemäß einige Zeit an.| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBSEEDING_OPERATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DEADLOCK_ENUM_MUTEX |Tritt auf, wenn die deadlocküberwachung und Sys. dm_os_waiting_tasks sicherstellen, dass SQL Server nicht mehrere deadlocksuchvorgänge gleichzeitig ausgeführt wird.| 
|DEADLOCK_TASK_SEARCH |Eine lange Wartezeit für diese Ressource zeigt an, dass der Server Abfragen zusätzlich zu sys.dm_os_waiting_tasks ausführt und diese Abfragen die Ausführung einer Deadlocksuche durch die Deadlocküberwachung blockieren. Dieser Wartetyp wird nur von der Deadlocküberwachung verwendet. Für Abfragen zusätzlich zu sys.dm_os_waiting_tasks wird DEADLOCK_ENUM_MUTEX verwendet.| 
|DEBUG |Tritt während der Transact-SQL und CLR-Debuggen für eine interne Synchronisierung.| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_POLL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_SYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISABLE_VERSIONING |Tritt auf, wenn SQL Server, die Version Transaktions-Manager abruft, um festzustellen, ob der Zeitstempel der ältesten aktiven Transaktion als der Zeitstempel liegt des bei der Statuswechsel begonnen hat. Wenn dies der Fall ist, sind alle Momentaufnahmetransaktionen abgeschlossen, die vor dem Ausführen der ALTER DATABASE-Anweisung begonnen wurden. Dieser Wartestatus wird verwendet, wenn SQL Server deaktiviert die versionsverwaltung mithilfe der ALTER DATABASE-Anweisung.| 
|DISKIO_SUSPEND |Tritt auf, wenn ein Task auf den Zugriff auf eine Datei wartet, wenn eine externe Sicherung aktiviert ist. Dieser Wartetyp wird für jeden wartenden Benutzerprozess gemeldet. Ein Wert über fünf pro Benutzerprozess kann darauf hinweisen, dass die externe Sicherung zu lange dauert.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISPATCHER_QUEUE_SEMAPHORE |Tritt auf, wenn ein Thread aus dem Verteilerpool auf weitere Arbeit wartet. Die Wartezeit für diesen Wartetyp steigt voraussichtlich, wenn der Verteiler im Leerlauf ist.| 
|DLL_LOADING_MUTEX |Tritt einmal auf, während auf das Laden der DLL des XML-Parsers gewartet wird.| 
|DPT_ENTRY_LOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROPTEMP |Tritt zwischen den Versuchen, ein temporäres Objekt zu löschen, auf, wenn beim vorherigen Versuch ein Fehler aufgetreten ist. Die Wartedauer nimmt mit jedem fehlerhaften Löschversuch exponentiell zu.| 
|DTC |Tritt auf, wenn ein Task auf ein Ereignis wartet, das für die Verwaltung des Statusübergangs verwendet wird. Dieser Zustand steuert, wenn die Wiederherstellung von Transaktionen von Microsoft Distributed Transaction Coordinator (MS DTC) auftritt, nachdem SQL Server erhält eine Benachrichtigung, dass der MS DTC-Dienst nicht verfügbar ist.| 
|DTC_ABORT_REQUEST |Tritt in einer MS DTC-Arbeitsthreadsitzung auf, wenn die Sitzung darauf wartet, eine MS DTC-Transaktion in Besitz zu nehmen. Sobald MS DTC die Transaktion besitzt, kann die Sitzung ein Rollback der Transaktion ausführen. Im Allgemeinen wartet die Sitzung auf eine andere Sitzung, die die Transaktion verwendet.| 
|DTC_RESOLVE |Tritt auf, wenn ein Wiederherstellungstask auf die master-Datenbank in einer datenbankübergreifenden Transaktion wartet, damit der Task das Ergebnis der Transaktion abfragen kann.| 
|DTC_STATE |Tritt auf, wenn ein Task auf ein Ereignis wartet, das Änderungen am internen globalen Statusobjekt für MS DTC schützt. Dieser Status sollte nur sehr kurze Zeit andauern.| 
|DTC_TMDOWN_REQUEST |Tritt auf, in einer MS DTC-arbeitsthreadsitzung, wenn SQL Server benachrichtigt, dass der MS DTC-Dienst nicht verfügbar ist. Zunächst wartet der Arbeitsthread auf den Beginn des MS DTC-Wiederherstellungsprozesses. Dann wartet der Arbeitsthread darauf, das Ergebnis der verteilten Transaktion, an der der Arbeitsthread arbeitet, abrufen zu können. Dies kann so lange fortgesetzt werden, bis die Verbindung mit dem MS DTC-Dienst wiederhergestellt ist.| 
|DTC_WAITFOR_OUTCOME |Tritt auf, wenn Wiederherstellungstasks darauf warten, dass MS DTC aktiviert wird, damit vorbereitete Transaktionen aufgelöst werden können.| 
|DTCNEW_ENLIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_PREPARE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_RECOVERY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TM |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCPNTSYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DUMP_LOG_COORDINATOR |Tritt auf, wenn ein Haupttask darauf wartet, dass ein untergeordneter Task Daten generiert. Normalerweise tritt dieser Status nicht auf. Eine lange Wartezeit weist auf eine unerwartete Blockierung hin. In diesem Fall sollte der untergeordnete Task überprüft werden.| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|EC |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|EE_PMOLOCK |Tritt bei der Synchronisierung bestimmter Typen von Speicherbelegungen während der Ausführung von Anweisungen auf.| 
|EE_SPECPROC_MAP_INIT |Tritt bei der Synchronisierung der Erstellung der internen Prozedurhashtabelle auf. Dieser Wartevorgang kann nur auftreten, während der ersten Zugriff auf die Hashtabelle nach dem Start von SQL Server-Instanz.| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ENABLE_VERSIONING |Tritt auf, wenn SQL Server wartet, bis alle Updatetransaktionen in dieser Datenbank abgeschlossen ist, bevor Sie deklarieren die Datenbank für den Übergang zum Status der Snapshot-Isolation bereit. Dieser Status wird verwendet, wenn SQL Server Snapshot-Isolation mithilfe der ALTER DATABASE-Anweisung aktiviert.| 
|ERROR_REPORTING_MANAGER |Tritt bei der Synchronisierung mehrerer gleichzeitiger Fehlerprotokollinitialisierungen auf.| 
|EXCHANGE |Tritt während der Synchronisierung des Austauschiterators des Abfrageprozessors während paralleler Abfragen auf.| 
|EXECSYNC |Tritt während paralleler Abfragen bei der Synchronisierung im Abfrageprozessor in Bereichen auf, die nicht mit dem Austauschiterator verbunden sind. Beispiele für solche Bereiche sind Bitmaps, LOBs (Large Objects) und der Spooliterator. Dieser Wartestatus kann von LOBs häufig verwendet werden.| 
|EXECUTION_PIPE_EVENT_INTERNAL |Tritt während der Synchronisierung zwischen den Producer- und Consumerteilen der Batchausführung auf, die über den Verbindungskontext gesendet werden.| 
|EXTERNAL_RG_UPDATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] über aktuelle.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_WAIT_ON_LAUNCHER, |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FAILPOINT |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FCB_REPLICA_READ |Tritt bei der Synchronisierung der Lesevorgänge einer Sparsedatei der Momentaufnahme (oder einer von DBCC erstellten temporären Momentaufnahme) auf.| 
|FCB_REPLICA_WRITE |Tritt beim Synchronisieren der Push- oder Pullvorgänge einer Seite in eine Sparsedatei der Momentaufnahme (oder einer von DBCC erstellten temporären Momentaufnahme) auf.| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_FIND |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_PARENT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_STATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FILEOBJECT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_TABLE_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NTFS_STORE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RECOVERY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_COMM |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_DB |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_TABLE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILE_VALIDATION_THREADS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CACHE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FCB |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILETABLE_SHUTDOWN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FOREIGN_REDO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] über aktuelle.| 
|FORWARDER_TRANSITION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FS_FC_RWLOCK |Tritt bei einem Wartevorgang auf die Durchführung einer der beiden folgenden Aktionen durch den FILESTREAM-Garbage Collector auf:| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |Tritt auf, wenn der FILESTREAM-Garbage Collector auf das Abschließen von Cleanuptasks wartet.| 
|FS_HEADER_RWLOCK |Tritt bei einem Wartevorgang auf den Erhalt von Zugriff auf den FILESTREAM-Header eines FILESTREAM-Datencontainers auf, um entweder Inhalte in der FILESTREAM-Headerdatei (Filestream.hdr) zu lesen oder zu aktualisieren.| 
|FS_LOGTRUNC_RWLOCK |Tritt bei einem Wartevorgang auf den Erhalt von Zugriff auf die FILESTREAM-Protokollkürzung auf, um eine der beiden folgenden Aktionen auszuführen:| 
|FSA_FORCE_OWN_XACT |Tritt auf, wenn ein FILESTREAM-Datei-E/A-Vorgang an die zugeordnete Transaktion gebunden werden muss, die Transaktion jedoch gerade im Besitz einer anderen Sitzung ist.| 
|FSAGENT |Tritt auf, wenn ein FILESTREAM-Datei-E/A-Vorgang auf eine FILESTREAM-Agent-Ressource wartet, die gerade von einem anderen Datei-E/A-Vorgang verwendet wird.| 
|FSTR_CONFIG_MUTEX |Tritt bei einem Wartevorgang auf eine andere Neukonfiguration eines FILESTREAM-Funktionen auf, die abgeschlossen werden soll.| 
|FSTR_CONFIG_RWLOCK |Tritt bei einem Wartevorgang auf die Serialisierung des Zugriffs auf die FILESTREAM-Konfigurationsparameter auf.| 
|FT_COMPROWSET_RWLOCK |Volltext wartet auf Metadatenvorgang für Fragment. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FT_IFTS_RWLOCK |Volltext wartet auf interne Synchronisierung. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FT_IFTS_SCHEDULER_IDLE_WAIT |Volltext-Wartetyp für den Ruhezustand des Zeitplanungsmoduls. Das Zeitplanungsmodul befindet sich im Leerlauf.| 
|FT_IFTSHC_MUTEX |Volltext wartet auf einen fdhost-Steuerungsvorgang. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FT_IFTSISM_MUTEX |Volltext wartet auf einen Kommunikationsvorgang. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FT_MASTER_MERGE |Volltext wartet auf Masterzusammenführungsvorgang. Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_METADATA_MUTEX |Wird nur für Informationszwecke dokumentiert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_RESTART_CRAWL |Tritt auf, wenn ein Volltextcrawl von einem letzten bekannten fehlerfreien Punkt neu gestartet werden muss, um nach einem vorübergehenden Fehler wiederhergestellt zu werden. Durch die Wartezeit können die Arbeitstasks, die zurzeit an der jeweiligen Auffüllung arbeiten, abgeschlossen werden oder den aktuellen Schritt beenden.| 
|FULLTEXT GATHERER |Tritt bei der Synchronisierung von Volltextvorgängen auf.| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_CREATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GUARDIAN |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|HADR_AG_MUTEX |Tritt auf, wenn eine AlwaysOn-DDL-Anweisung oder der Windows Server-failoverclusteringbefehl auf exklusiven Lese-/Schreibzugriff auf die Konfiguration einer verfügbarkeitsgruppe wartet., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Tritt auf, wenn eine AlwaysOn-DDL-Anweisung oder der Windows Server-failoverclusteringbefehl auf exklusiven Lese-/Schreibzugriff auf den Laufzeitstatus des lokalen Replikats der zugeordneten verfügbarkeitsgruppe wartet., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_MANAGER_MUTEX |Tritt auf, wenn das Herunterfahren eines Verfügbarkeitsreplikats auf das Abschließen des Startvorgangs wartet oder wenn der Start eines Verfügbarkeitsreplikats auf das Abschließen des Herunterfahrens wartet. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |Der Verleger für ein Verfügbarkeitsreplikatereignis (z. B. eine Statusänderung oder eine Konfigurationsänderung) wartet auf exklusiven Lese-/Schreibzugriff für die Liste der Ereignisabonnenten. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_BULK_LOCK |Die Always On-primäre Datenbank empfangen eine Anforderung für die Sicherung von einer sekundären Datenbank und wartet darauf, für den Hintergrund des Threads für die Verarbeitung der Anforderung zum Abrufen oder Aufheben der BulkOp-Sperre abgeschlossen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_QUEUE |Der sicherungshintergrundthread der primären-Datenbank immer auf wartet darauf, dass eine neue arbeitsanforderung von der sekundären Datenbank. (in der Regel wird dies tritt auf, wenn die primäre Datenbank das BulkOp-Protokoll enthalten ist und wartet darauf, dass die sekundäre Datenbank aus, um anzugeben, dass die primäre Datenbank die Sperre aufheben kann)., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CLUSAPI_CALL |Ein SQL Server-Thread wartet auf vom nicht präemptiven Modus (von SQL Server geplant) in den präemptiven Modus (vom Betriebssystem geplant) wechseln, um Windows Server Failover Clustering-APIs aufzurufen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_COMPRESSED_CACHE_SYNC |Warten auf Zugriff auf den Cache komprimierten Protokollblöcken, die verwendet wird, vermeiden Sie redundante Komprimierung der Protokollblöcke, die an mehrere sekundäre Datenbanken gesendet., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_FLOW_CONTROL |Warten, dass Meldungen an den Partner gesendet werden, wenn die maximale Anzahl von Meldungen in der Warteschlange erreicht wurde. Gibt an, dass die Protokollscans schneller ausgeführt werden als Netzwerksendevorgänge. Dies ist ein Problem, nur dann, wenn Netzwerksendevorgänge langsamer als erwartet werden., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_VERSIONING_STATE |Tritt bei der versionsstatusänderung einer Always On-sekundären Datenbank. Dieser Wartetyp wird für interne Datenstrukturen und ist in der Regel sehr kurz und hat keine direkten Auswirkungen auf den Datenzugriff ist., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RESTART |Es wird darauf gewartet, dass AlwaysOn-Verfügbarkeitsgruppen kontrolliert einen Neustart der Datenbank. Unter normalen Bedingungen ist dies nicht Problem für Kunden, da Wartezeiten hier erwartet werden., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Eine Abfrage für Objekte in einer lesbaren sekundären Datenbank von einer Always On-verfügbarkeitsgruppe auf der zeilenversionsverwaltung blockiert wird, während des Wartens auf ein Commit oder Rollback für alle Transaktionen, die noch nicht gespeichert waren, wenn das sekundäre Replikat für lesearbeitslasten aktiviert wurde. Dieser Wartetyp garantiert, dass Zeilenversionen vor der Ausführung einer Abfrage unter der momentaufnahmeisolation verfügbar sind., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_COMMAND |Warten auf Antworten auf dialogorientierte Nachrichten (die eine explizite Antwort von der anderen Seite mithilfe der Infrastruktur für das Always On-natürlichsprachliches Nachricht erfordern). Eine Anzahl von unterschiedlichen Nachrichtentypen verwendet diesen Wartetyp., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_COMPLETION_SYNC |Warten auf Antworten auf dialogorientierte Nachrichten (die eine explizite Antwort von der anderen Seite mithilfe der Infrastruktur für das Always On-natürlichsprachliches Nachricht erfordern). Eine Anzahl von unterschiedlichen Nachrichtentypen verwendet diesen Wartetyp., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_START_SYNC |Eine AlwaysOn-DDL-Anweisung oder einen Windows Server Failover Clustering-Befehl wartet auf serialisierten Zugriff auf eine verfügbarkeitsdatenbank und deren Laufzeitstatus., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER |Der Verleger für ein Verfügbarkeitsreplikatereignis (z. B. eine Statusänderung oder eine Konfigurationsänderung) wartet auf exklusiven Lese-/Schreibzugriff auf den Laufzeitstatus eines Ereignisabonnenten, der einer Verfügbarkeitsdatenbank entspricht. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |Der Verleger für ein Verfügbarkeitsreplikatereignis (z. B. eine Statusänderung oder eine Konfigurationsänderung) wartet auf exklusiven Lese-/Schreibzugriff auf die Liste von Ereignisabonnenten, die Verfügbarkeitsdatenbanken entsprechen. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSTATECHANGE_SYNC |Parallelität Steuerelement Wartevorgang zum Aktualisieren des internen Zustands des datenbankreplikats., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FABRIC_CALLBACK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_BLOCK_FLUSH |Der FILESTREAM Always On-Transport-Manager wartet, bis die Verarbeitung eines protokollblocks abgeschlossen ist., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_CLOSE |Der FILESTREAM Always On-Transport-Manager wartet, bis die nächste FILESTREAM-Datei verarbeitet wird, und ihr Handle geschlossen wird., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_REQUEST |Always On sekundäres Replikat wartet darauf, dass das primäre Replikat alle angeforderten FILESTREAM senden Dateien während UNDO., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR |Der FILESTREAM Always On-Transport-Manager wartet darauf, dass R/W-Sperre, die den FILESTREAM immer auf e/a-Manager während des Starts oder Herunterfahrens schützt., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |Der FILESTREAM immer auf e/a-Manager wartet auf den Abschluss von e/a-., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_MANAGER |Der FILESTREAM Always On-Transport-Manager wartet darauf, dass die R/W-Sperre, die den FILESTREAM Always On-Transport-Manager während des Starts oder Herunterfahrens schützt., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_GROUP_COMMIT |Die Transaktionscommitverarbeitung wartet auf das Zulassen eines Gruppencommits, damit mehrere Protokolldatensätze für den Commit in einen einzelnen Protokollblock gesetzt werden können. Dieser Wartetyp ist eine erwartete Bedingung, die das Protokoll-e/a optimiert, erfassen und Transportsendevorgängen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_SYNC |Parallelitätssteuerung um die Protokollaufzeichnung oder Anwendungsobjekt beim Erstellen von Löschen von Scans. Dies ist ein erwarteter Wartevorgang, wenn Partner Status oder Verbindungsstatus ändern., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_WAIT |Warten, bis Protokolldatensätze verfügbar werden. Kann beim Warten auf die Erstellung von neuen Protokolldatensätzen durch Verbindungen oder auf den E/A-Abschluss generiert werden, wenn das Lesen des Protokolls nicht im Cache stattfindet. Dies ist ein erwarteter Wartevorgang, wenn der Protokollscan das Ende des Protokolls aufgeholt ist oder vom Datenträger liest., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGPROGRESS_SYNC |Parallelität Steuerelement Wartevorgang beim Aktualisieren des Protokollstatus von Datenbankreplikaten., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_DEQUEUE |Ein Hintergrundtask, der Windows Server-Failoverclusteringbenachrichtigungen verarbeitet und auf die nächste Benachrichtigung wartet. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |Der AlwaysOn-verfügbarkeitsreplikat-Manager wartet auf serialisierten Zugriff auf den Laufzeitstatus eines Hintergrundtasks, der Windows Server-failoverclusteringbenachrichtigungen verarbeitet. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |Ein Hintergrundtask wartet auf den Abschluss des Starts eines Hintergrundtasks, der Windows Server-Failoverclusteringbenachrichtigungen verarbeitet. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |Ein Hintergrundtask wartet auf den Abschluss eines Hintergrundtasks, der Windows Server-Failoverclusteringbenachrichtigungen verarbeitet. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_PARTNER_SYNC |Parallelität Steuerelement Wartevorgang für der Partnerliste., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_READ_ALL_NETWORKS |Wartet auf Lese- oder Schreibzugriff für die List mit WSFC-Netzwerken. Nur interne Verwendung. Hinweis: Das Modul führt eine Liste der wsfc-Netzwerken, die verwendet wird, wird in dynamischen Verwaltungssichten (z. B. sys. dm_hadr_cluster_networks) oder zur Überprüfung immer in Transact-SQL-Anweisungen, die WSFC verweisen Netzwerkinformationen. Diese Liste wird aktualisiert, nach Modulstart, WSFC-bezogene Benachrichtigungen und internen AlwaysOn-Neustart (z. B. verlieren und Wiedererlangen des wsfc-Quorums). Tasks werden normalerweise blockiert, wenn ein Update in dieser Liste ausgeführt wird. , <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |Warten, bis die sekundäre Datenbank vor dem Ausführen der Wiederherstellung eine Verbindung mit der primären Datenbank herstellt. Dies ist ein erwarteter Wartevorgang, der länger dauern kann, wenn die Verbindung mit dem primären Replikat nur langsam aufgebaut wird., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_UNDO |Die Datenbankwiederherstellung wartet, bis die sekundäre Datenbank die Wiederherstellungs- und Initialisierungsphase beendet hat, um diese mit der primären Datenbank auf den allgemeinen Protokollpunkt zurückzubringen. Dies ist ein erwarteter Wartevorgang nach Failovers. Rückgängig machen Fortschritt über die Windows-Systemmonitor (perfmon.exe) und dynamischen Verwaltungssichten nachverfolgt werden kann., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_REPLICAINFO_SYNC |Warten auf die parallelitätssteuerung den aktuellen Replikatstatus aktualisiert., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNC_COMMIT |Warten auf die Transaktionscommitverarbeitung, bis die synchronisierten sekundären Datenbanken das Protokoll härten. Dieser Wartevorgang wird auch durch den Leistungsindikator für die Transaktionsverzögerung wiedergegeben. Dieser Wartetyp wird erwartet synchronisiert Verfügbarkeit gruppiert und gibt die Zeit zum Senden, schreiben und bestätigen des Protokolls an die sekundären Datenbanken., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNCHRONIZING_THROTTLE |Warten, bis die Transaktionscommitverarbeitung erlaubt, dass eine synchronisierende sekundäre Datenbank das primäre Ende des Protokolls erreicht, um in den synchronisierten Status überzugehen. Dies ist ein erwarteter Wartevorgang, wenn eine sekundäre Datenbank im Rückstand ist., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC |Das interne AlwaysOn-System oder der wsfc-Cluster fordert, dass Listener gestartet oder beendet werden. Die Verarbeitung dieser Anforderung ist immer asynchron, und es gibt einen Mechanismus zum Entfernen von redundanten Anforderungen. Es gibt auch Momente, in denen dieser Prozess aufgrund von Konfigurationsänderungen angehalten wird. Alle Wartevorgänge, die mit diesem Listener-Synchronisierungsmechanismus verknüpft sind, verwenden diesen Wartetyp. Nur zur internen Verwendung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |Am Ende einer immer auf Transact-SQL-Anweisung, die erforderlich sind, starten und/oder beenden Anavailability den Listener verwendet. Da der Start-/Beendigungsvorgang asynchron erfolgt, der UI-Thread blockiert mit diesem Wartetyp, bis die Situation des Listeners bekannt ist., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TIMER_TASK |Warten auf die Sperre für das Zeitgebertaskobjekt; wird auch für die tatsächlichen Wartevorgänge zwischen Zeiten verwendet, in denen Arbeiten ausgeführt werden. Z. B. für eine Aufgabe, die alle 10 Sekunden, nach einer Ausführung ausgeführt wird-AlwaysOn-Verfügbarkeitsgruppen, ca. 10 Sekunden auf der Task erneut geplant wartet, und die Wartezeit ist darin enthalten., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_DBRLIST |Warten auf Zugriff auf die Datenbankreplikatliste der Transportschicht. Für den Spinlock, die Zugriff darauf verwendet., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_FLOW_CONTROL |Warten, wenn die Anzahl der ausstehenden unbestätigten Always On-Nachrichten über die Out Schwellenwert für die flusssteuerung. Dies ist auf Verfügbarkeit replikatreplikats-Basis (nicht auf eine Datenbank-Basis)., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_SESSION |AlwaysOn-Verfügbarkeitsgruppen wartet darauf, beim Ändern oder den Zugriff auf die zugrunde liegende Transportstatus., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_POOL |Parallelität Steuerelement warten auf das Taskobjekt der Hintergrundarbeit AlwaysOn-Verfügbarkeitsgruppen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_QUEUE |AlwaysOn-Verfügbarkeitsgruppen Hintergrundarbeitsthread werden Zuweisung neuer Arbeit wartet. Dies ist ein erwarteter Wartevorgang, wenn vorhanden sind Arbeitsthreads warten auf neue Arbeit, die den Zustand "normal" ist., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_XRF_STACK_ACCESS |Zugreifen (suchen, hinzufügen und löschen) der Stapel für eine Always On-verfügbarkeitsdatenbank erweiterten wiederherstellungsverzweigung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HCCO_CACHE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HK_RESTORE_FILEMAP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTBUILD |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTDELETE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTMEMO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREINIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREPARTITION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTTP_ENUMERATION |Tritt beim Starten auf, wenn die HTTP-Endpunkte zum Starten von HTTP aufgezählt werden sollen.| 
|HTTP_START |Tritt auf, wenn eine Verbindung auf den Abschluss der HTTP-Initialisierung wartet.| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IMPPROV_IOWAIT |Tritt auf, wenn SQL Server wartet, bis eine Bulkload e/a, um den Vorgang abzuschließen.| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|INTERNAL_TESTING |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|IO_AUDIT_MUTEX |Tritt während der Synchronisierung von Ereignispuffern der Ablaufverfolgung auf.| 
|IO_COMPLETION |Tritt auf, während auf den Abschluss von E/A-Vorgängen gewartet wird. Dieser Wartetyp stellt in der Regel Nicht-Datenseiten-E/A-Vorgänge dar. Für Datenseiten e/a Abschluss werden angezeigt als PAGEIOLATCH\_ \* wartet.| 
|IO_QUEUE_LIMIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IO_RETRY |Tritt auf, wenn ein E/A-Vorgang, z. B. das Lesen von oder Schreiben auf einen Datenträger, aufgrund unzureichender Ressourcen scheitert und dann wiederholt wird.| 
|IOAFF_RANGE_QUEUE |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|KSOURCE_WAKEUP |Wird vom Dienststeuerungstask verwendet, während auf Anforderungen vom Dienstkontroll-Manager gewartet wird. Lange Wartezeiten werden erwartet und zeigen kein Problem an.| 
|KTM_ENLISTMENT |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|KTM_RECOVERY_MANAGER |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|KTM_RECOVERY_RESOLUTION |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|LATCH_DT |Tritt beim Warten auf einen DT-Latch (Löschlatch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste der LATCH\_ \* Wartevorgänge ist in Sys. dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.| 
|LATCH_EX |Tritt beim Warten auf einen EX-Latch (exklusiven Latch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste der LATCH\_ \* Wartevorgänge ist in Sys. dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.| 
|LATCH_KP |Tritt beim Warten auf einen KP-Latch (Beibehaltungslatch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste der LATCH\_ \* Wartevorgänge ist in Sys. dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.| 
|LATCH_NL |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|LATCH_SH |Tritt beim Warten auf einen SH-Latch (gemeinsamen Latch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste der LATCH\_ \* Wartevorgänge ist in Sys. dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.| 
|LATCH_UP |Tritt beim Warten auf einen UP-Latch (Updatelatch) auf. Dazu gehören keine Pufferlatches oder Transaktionsmarkierungslatches. Eine Liste der LATCH\_ \* Wartevorgänge ist in Sys. dm_os_latch_stats verfügbar. Beachten Sie, dass sys.dm_os_latch_stats die Wartevorgänge LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX und LATCH_DT in einer Gruppe zusammenfasst.| 
|LAZYWRITER_SLEEP |Tritt auf, wenn Tasks für verzögertes Schreiben angehalten werden. Dieser Wartetyp gibt die Zeitdauer von wartenden Hintergrundtasks an. Wenn Sie nach durch den Benutzer bedingtem Hängen des Computers suchen, sollten Sie diesen Status nicht verwenden.| 
|LCK_M_BU |Tritt auf, wenn ein Task darauf wartet, eine Massenupdatesperre (BU-Sperre) abzurufen.| 
|LCK_M_BU_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine Massenupdatesperre (BU-Sperre) mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_BU_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine Massenupdatesperre (BU-Sperre) mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte gemeinsame Sperre (IS-Sperre) abzurufen.| 
|LCK_M_IS_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte gemeinsame Sperre (IS-Sperre) mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte gemeinsame Sperre (IS-Sperre) mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte Updatesperre (IU-Sperre) abzurufen.| 
|LCK_M_IU_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte Updatesperre (IU-Sperre) mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte Updatesperre (IU-Sperre) mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte exklusive Sperre (IX-Sperre) abzurufen.| 
|LCK_M_IX_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte exklusive Sperre (IX-Sperre) mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine beabsichtigte exklusive Sperre (IX-Sperre) mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL |Tritt auf, wenn ein Task darauf wartet, eine NULL-Sperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Eine NULL-Sperre für den Schlüssel ist eine Sperre, die sofort aufgehoben wird.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine NULL-Sperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine Einfügungssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Eine NULL-Sperre für den Schlüssel ist eine Sperre, die sofort aufgehoben wird. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine NULL-Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine Einfügungssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. Eine NULL-Sperre für den Schlüssel ist eine Sperre, die sofort aufgehoben wird. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine Einfügungssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine Einfügungssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U |Ein Task wartet darauf, eine Updatesperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |Task wartet darauf, eine Updatesperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine Einfügungssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U_LOW_PRIORITY |Task wartet darauf, eine Updatesperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine Einfügungssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre für den aktuellen Schlüsselwert und eine Einfügungssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine Einfügungssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine Einfügungssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre für den aktuellen Schlüsselwert und eine freigegebene Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RS_S_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine freigegebene Bereichssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine freigegebene Bereichssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre für den aktuellen Schlüsselwert und eine Bereichsupdatesperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RS_U_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine Updatebereichssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine Einfügungssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre für den aktuellen Schlüsselwert und eine exklusive Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RX_S_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine exklusive Bereichssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine exklusive Bereichssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre für den aktuellen Schlüsselwert und eine exklusive Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RX_U_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine exklusive Bereichssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine exklusive Bereichssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre für den aktuellen Schlüsselwert und eine exklusive Bereichssperre zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen.| 
|LCK_M_RX_X_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit Abbruchs-Blockern für den aktuellen Schlüsselwert und eine exklusive Bereichssperre mit Abbruchs-Blockern zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit niedriger Priorität für den aktuellen Schlüsselwert und eine exklusive Bereichssperre mit niedriger Priorität zwischen dem aktuellen und dem vorherigen Schlüssel abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre abzurufen.| 
|LCK_M_S_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M |Tritt auf, wenn ein Task darauf wartet, eine Schemaänderungssperre abzurufen.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine Schemaänderungssperre Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine Schemaänderungssperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Schemasperre abzurufen.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Schemasperre Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Schemasperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter Updatesperre abzurufen.| 
|LCK_M_SIU_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter Updatesperre mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter Updatesperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter exklusiver Sperre abzurufen.| 
|LCK_M_SIX_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter exklusiver Sperre mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine gemeinsame Sperre mit beabsichtigter exklusiver Sperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre abzurufen.| 
|LCK_M_U_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit beabsichtigter exklusiver Sperre abzurufen.| 
|LCK_M_UIX_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit beabsichtigter exklusiver Sperre mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine Updatesperre mit beabsichtigter exklusiver Sperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre abzurufen.| 
|LCK_M_X_ABORT_BLOCKERS |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit Abbruchs-Blockern abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X_LOW_PRIORITY |Tritt auf, wenn ein Task darauf wartet, eine exklusive Sperre mit niedriger Priorität abzurufen. (In Bezug auf die wartevorgangsoption mit niedriger Priorität von ALTER TABLE und ALTER INDEX.), <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_POOL_SCAN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_RATE_GOVERNOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGBUFFER |Tritt auf, wenn ein Task auf Speicherplatz im Protokollpuffer zum Speichern eines Protokolldatensatzes wartet. Durchgehend hohe Werte können darauf hinweisen, dass die Protokollgeräte die Menge der vom Server generierten Protokolldaten nicht bewältigen können.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGGENERATION |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|LOGMGR |Tritt auf, wenn ein Task beim Schließen der Datenbank vor dem Beenden des Protokolls auf das Fertigstellen ausstehender Protokoll-E/A-Vorgänge wartet.| 
|LOGMGR_FLUSH |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|LOGMGR_PMM_LOG |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGMGR_QUEUE |Tritt auf, während der Protokollschreibertask auf Arbeitsanforderungen wartet.| 
|LOGMGR_RESERVE_APPEND |Tritt auf, wenn ein Task darauf wartet, feststellen zu können, ob durch das Abschneiden von Protokollen Speicherplatz freigegeben wird, damit der Task einen neuen Protokolldatensatz schreiben kann. Erwägen Sie, die Größe der Protokolldatei(en) für die betroffene Datenbank zu erhöhen, um diese Wartezeit zu reduzieren.| 
|LOGPOOL_CACHESIZE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMERSET |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_FREEPOOLS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_MGRSET |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOWFAIL_MEMMGR_QUEUE |Tritt auf, während darauf gewartet wird, dass Arbeitsspeicher zur Verwendung verfügbar ist.| 
|MD_AGENT_YIELD |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_ALLOCATION_EXT |Tritt auf beim belegen von Arbeitsspeicher von den internen SQL Server-Speicher-Pool oder des Betriebssystems,., <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_GRANT_UPDATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|MIGRATIONBUFFER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MISCELLANEOUS |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|MISCELLANEOUS |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|MSQL_DQ |Tritt auf, wenn ein Task auf das Ende eines verteilten Abfragevorgangs wartet. Dieser Wartetyp wird verwendet, um mögliche MARS-Anwendungsdeadlocks (Multiple Active Result Sets) zu erkennen. Die Wartezeit wird mit dem Ende des Aufrufs der verteilten Abfrage beendet.| 
|MSQL_XACT_MGR_MUTEX |Tritt auf, wenn ein Task darauf wartet, in den Besitz des Sitzungstransaktions-Managers zu gelangen, um einen Transaktionsvorgang auf Sitzungsebene auszuführen.| 
|MSQL_XACT_MUTEX |Tritt während der Synchronisierung der Transaktionsverwendung auf. Eine Anforderung muss den Mutex abrufen, bevor sie die Transaktion verwenden kann.| 
|MSQL_XP |Tritt auf, wenn ein Task auf das Ende einer erweiterten gespeicherten Prozedur wartet. SQL Server verwendet diesen Wartestatus, um mögliche MARS-anwendungsdeadlocks zu erkennen. Die Wartezeit wird mit dem Ende des Aufrufs der erweiterten gespeicherten Prozedur beendet.| 
|MSSEARCH |Tritt während Aufrufen der Volltextsuche auf. Diese Wartezeit endet, wenn der Volltextvorgang abgeschlossen ist. Sie zeigt keinen Konflikt an, sondern die Dauer von Volltextvorgängen.| 
|NET_WAITFOR_PACKET |Tritt auf, wenn eine Verbindung während eines Netzwerklesevorgangs auf ein Netzwerkpaket wartet.| 
|NETWORKSXMLMGRLOAD |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |Tritt auf, wenn SQL Server den SQL Server Native Client OLE DB-Anbieter aufruft. Dieser Wartetyp wird nicht für die Synchronisierung verwendet. Er zeigt vielmehr die Dauer von Aufrufen des OLE DB-Anbieters an.| 
|ONDEMAND_TASK_QUEUE |Tritt auf, während ein Hintergrundtask auf Systemtaskanforderungen mit hoher Priorität wartet. Lange Wartezeiten zeigen an, dass keine Anforderungen mit hoher Priorität zu verarbeiten waren, und sollten kein Problem darstellen.| 
|PAGEIOLATCH_DT |Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Löschmodus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.| 
|PAGEIOLATCH_EX |Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im exklusiven Modus: Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.| 
|PAGEIOLATCH_KP |Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Beibehaltungsmodus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.| 
|PAGEIOLATCH_NL |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PAGEIOLATCH_SH |Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im freigegebenen Modus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.| 
|PAGEIOLATCH_UP |Tritt auf, wenn ein Task auf einen Latch für einen Puffer in einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Updatemodus. Lange Wartezeiten können Probleme mit dem Datenträgersubsystem anzeigen.| 
|PAGELATCH_DT |Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Löschmodus.| 
|PAGELATCH_EX |Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im exklusiven Modus:| 
|PAGELATCH_KP |Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Beibehaltungsmodus.| 
|PAGELATCH_NL |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PAGELATCH_SH |Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im freigegebenen Modus.| 
|PAGELATCH_UP |Tritt auf, wenn ein Task auf einen Latch für einen Puffer außerhalb einer E/A-Anforderung wartet. Die Latchanforderung erfolgt im Updatemodus.| 
|PARALLEL_BACKUP_QUEUE |Tritt beim Serialisieren der Ausgabe auf, die von RESTORE HEADERONLY, RESTORE FILELISTONLY oder RESTORE LABELONLY erstellt wurde.| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_ABR |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Tritt auf, wenn das Zeitplanungsmodul für das [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Betriebssystem (SQLOS) in den präemptiven Modus wechselt, um ein Überwachungsereignis in das Windows-Ereignisprotokoll zu schreiben. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein Überwachungsereignis in das Windows-Sicherheitsprotokoll zu schreiben. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um Sicherungsmedien zu schließen.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein Bandsicherungsmedium zu schließen.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein virtuelles Sicherungsmedium zu schließen.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um Windows-Failoverclustervorgänge auszuführen.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |Tritt auf, wenn das SQLOS-Zeitplanungsmodul in den präemptiven Modus wechselt, um ein COM-Objekt zu erstellen.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |CSS-Diagnose plant Lease-Manager für AlwaysOn-Verfügbarkeitsgruppen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] bis [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PREEMPTIVE_TESTING |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|PRINT_ROLLBACK_PROGRESS |Wird verwendet, um zu warten, während Benutzerprozesse in einer Datenbank beendet werden, die mithilfe der ALTER DATABASE-Beendigungsklausel von einem Status in einen anderen versetzt wurde. Weitere Informationen finden Sie unter "ALTER DATABASE (Transact-SQL)".| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_COOP_SCAN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |Tritt auf, wenn eine Hintergrundaufgabe für die Beendigung des Hintergrundtasks wartet, die empfängt (über Abruf) Windows Server-failoverclusteringbenachrichtigungen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CLUSTER_INTEGRATION |Eine Append, ersetzungs- und/oder Löschvorgang wartet auf eine Schreibsperre in einer Always On-internen Liste (z. B. eine Liste von Netzwerken, Netzwerkadressen oder verfügbarkeitsgruppenlistenern). Nur interne Verwendung <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_JOIN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_OFFLINE_COMPLETED |Eine AlwaysOn-Verfügbarkeit Gruppe Löschvorgang wartet darauf, dass die zielverfügbarkeitsgruppe offline geht, bevor Sie Windows Server Failover Clustering-Objekte zu zerstören., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ONLINE_COMPLETED |Erstellen einer Always On oder Failovervorgang Verfügbarkeit wartet darauf, dass die zielverfügbarkeitsgruppe online geschaltet., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Eine AlwaysOn-Verfügbarkeit Gruppe Löschvorgang wartet auf die Beendigung eines Hintergrundtasks, der als Teil eines vorherigen Befehls geplant wurde. Es darf z. B. einen Hintergrundtask geben, der Verfügbarkeitsdatenbanken an die primäre Rolle übergibt. Die DROP AVAILABILITY GROUP-DDL muss warten Abschluss dieses Hintergrundtasks beendet wird, um Racebedingungen zu verhindern., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_WORKITEM_COMPLETED |Interner Wartevorgang von einem Thread, der auf den Abschluss eines asynchronen Arbeitstasks wartet. Dies ist ein erwarteter Wartevorgang und ist für die Verwendung von CSS., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADRSIM |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_LOGIN_STATS |Tritt während der internen Synchronisierung in Metadaten zu Anmeldestatistiken., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_RELATION_CACHE |Tritt auf, während der internen Synchronisierung in Metadaten zu Tabelle oder eines Indexes., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_SERVER_CACHE |Tritt während der internen Synchronisierung in Metadaten zu Verbindungsservern auf., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_UPGRADE_CONFIG |Tritt während der internen Synchronisierung beim Aktualisieren von serverweiten Konfigurationen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_QUEUE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BCKG_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BLOOM_FILTER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CTXS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DB_DISK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DYN_VECTOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_HOST_INIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_LOADDB |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT_DISK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_SHUTDOWN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_START |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QE_WARN_LIST_SYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QPJOB_KILL |Weist darauf hin, dass das asynchrone automatische Update der Statistik durch den Aufruf von KILL beim Starten des Updates abgebrochen wurde. Der Abschlussthread wird angehalten, und es wird darauf gewartet, dass er mit dem Überwachen auf KILL-Befehle beginnt. Ein guter Wert liegt unter einer Sekunde.| 
|QPJOB_WAITFOR_ABORT |Weist darauf hin, dass das asynchrone automatische Update der Statistik durch den Aufruf von KILL während des Updates abgebrochen wurde. Das Update wurde jetzt beendet und wird so lange angehalten, bis die Nachrichtenkoordination des Abschlussthreads abgeschlossen ist. Dies ist ein gewöhnlicher, jedoch selten vorkommender Status, der sehr kurz sein sollte. Ein guter Wert liegt unter einer Sekunde.| 
|QRY_MEM_GRANT_INFO_MUTEX |Tritt auf, wenn die Arbeitsspeicherverwaltung für die Abfrageausführung den Zugriff auf statische Listen mit Informationen zu zugewiesenen Arbeitsspeichern steuert. Dieser Status listet Informationen zu den aktuellen zugewiesenen und wartenden Speicheranforderungen auf. Dieser Status ist ein einfacher Zugriffssteuerungsstatus. In diesem Status sollte es nie zu langen Wartezeiten kommen. Wird dieser Mutex nicht freigegeben, antworten alle neuen speicherbeanspruchenden Abfragen nicht mehr.| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_ERRHDL_SERVICE_DONE |Nur für Informationszwecke identifiziert. Nicht unterstützt. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|QUERY_WAIT_ERRHDL_SERVICE |Nur für Informationszwecke identifiziert.  Nicht unterstützt. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |Tritt in bestimmten Fällen auf, wenn eine Offlineindexerstellung parallel ausgeführt wird und die unterschiedlichen Arbeitsthreads, die die Sortierung ausführen, den Zugriff auf die Sortierungsdateien synchronisieren.| 
|QUERY_NOTIFICATION_MGR_MUTEX |Tritt während der Synchronisierung der Garbage Collection-Warteschlange im Abfragebenachrichtigungs-Manager auf.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |Tritt während der Statussynchronisierung für Transaktionen in Abfragebenachrichtigungen auf.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |Tritt während der internen Synchronisierung im Abfragebenachrichtigungs-Manager auf.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |Tritt während der Synchronisierung der Erstellung der Diagnoseausgabe des Abfrageoptimierers auf. Dieser Wartetyp tritt nur auf, wenn diagnoseeinstellungen unter der Richtung des Microsoft Support Services aktiviert wurden.| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_TRACEOUT |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|RBIO_WAIT_VLF |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RECOVER_CHANGEDB |Tritt während der Synchronisierung des Datenbankstatus in einer Datenbank im betriebsbereiten Standbymodus auf.| 
|RECOVERY_MGR_LOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_SYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_BLOCK_IO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_CACHE_ACCESS |Tritt während der Synchronisierung für einen Replikationsartikelcache auf. Während dieser Wartezeiten wird der Replikationsprotokollleser angehalten, und Anweisungen der Datendefinitionssprache (Data Definition Language, DDL) für eine veröffentlichte Tabelle werden blockiert.| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |Tritt während der Synchronisierung von Versionsinformationen des Replikationsschemas auf. Dieser Status ist vorhanden, wenn DDL-Anweisungen für das replizierte Objekt ausgeführt werden und wenn der Protokollleser ein versionsspezifisches Schema auf der Basis des Auftretens von DDL erstellt oder verwendet. Konflikte kann für diesen Wartetyp angezeigt werden, wenn Sie viele veröffentlichte Datenbanken auf einem Verleger mit der Transaktionsreplikation und der veröffentlichten Datenbanken sehr aktiv sind.| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPLICA_WRITES |Tritt auf, während ein Task auf den Abschluss von Seitenschreibvorgängen in Datenbankmomentaufnahmen oder DBCC-Replikaten wartet.| 
|REQUEST_DISPENSER_PAUSE |Tritt auf, wenn ein Task auf den Abschluss aller ausstehenden E/A-Vorgänge wartet, damit E/A-Vorgänge in eine Datei für eine Momentaufnahmesicherung eingefroren werden können.| 
|REQUEST_FOR_DEADLOCK_SEARCH |Tritt auf, während die Deadlocküberwachung darauf wartet, die nächste Deadlocksuche zu starten. Dieser Wartetyp wird zwischen Deadlockerkennungen erwartet, und eine lange Gesamtwartezeit für diese Ressource zeigt kein Problem an.| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESMGR_THROTTLED |Tritt auf, wenn eine neue Anforderung eingeht und auf der Basis der Einstellung GROUP_MAX_REQUESTS eingeschränkt wird.| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESOURCE_QUEUE |Tritt während der Synchronisierung verschiedener interner Ressourcenwarteschlangen auf.| 
|RESOURCE_SEMAPHORE |Tritt auf, wenn einer Arbeitsspeicheranforderung einer Abfrage aufgrund von anderen gleichzeitigen Abfragen nicht sofort entsprochen werden kann. Lange Wartevorgänge und Wartezeiten zeigen möglicherweise eine überhöhte Anzahl gleichzeitiger Abfragen oder eine überhöhte Menge angeforderten Arbeitsspeichers an.| 
|RESOURCE_SEMAPHORE_MUTEX |Tritt auf, während eine Abfrage darauf wartet, dass ihre Anforderung einer Threadreservierung erfüllt wird. Der Wartetyp tritt außerdem beim Synchronisieren von Abfragekompilierungs- und Arbeitsspeicherzuweisungsanforderungen auf.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |Tritt auf, wenn die Anzahl gleichzeitiger Abfragekompilierungen einen Drosselungsgrenzwert erreicht. Lange Wartevorgänge und Wartezeiten zeigen möglicherweise eine überhöhte Anzahl von Kompilierungen, Neukompilierungen oder nicht zwischenspeicherbaren Plänen an.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |Tritt auf, wenn einer Arbeitsspeicheranforderung einer kleinen Abfrage aufgrund von anderen gleichzeitigen Abfragen nicht sofort entsprochen werden kann. Die Wartezeit sollte wenige Sekunden nicht überschreiten, da der Server die Anforderung an den Hauptspeicherpool für Abfragen überträgt, wenn er den angeforderten Arbeitsspeicher nicht innerhalb weniger Sekunden erteilen kann. Lange Wartezeiten zeigen möglicherweise eine übermäßige Anzahl gleichzeitiger kleiner Abfragen bei gleichzeitiger Blockierung des Hauptspeicherpools durch wartende Abfragen an. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ROWGROUP_VERSION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RTDATA_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_CARGO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_DISPATCH |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_TRANSPORT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEC_DROP_TEMP_KEY |Tritt nach einem fehlerhaftem Versuch, einen temporären Sicherheitsschlüssel zu löschen, vor einem Wiederholungsversuch auf.| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_MUTEX |Tritt bei einem Wartevorgang auf Mutexe auf, die den Zugriff auf die globale Liste von EKM (Extensible Key Management)-Kryptografieanbietern und die Sitzungsbereichsliste der EKM-Sitzungen steuern.| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEMPLAT_DSI_BUILD |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENCE_GENERATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENTIAL_GUID |Tritt auf, während eine neue sequenzielle GUID empfangen wird.| 
|SERVER_IDLE_CHECK |Tritt auf, während der Synchronisierung des Leerlaufstatus für SQL Server-Instanz, wenn ein Ressourcenmonitor versucht, eine SQL Server-Instanz als im Leerlauf zu deklarieren oder reaktivierungsversuch.| 
|SERVER_RECONFIGURE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHUTDOWN |Tritt auf, während eine Anweisung zum Herunterfahren darauf wartet, dass aktive Verbindungen beendet werden.| 
|SLEEP_BPOOL_FLUSH |Tritt auf, wenn ein Prüfpunkt die Ausgabe neuer E/A-Vorgänge drosselt, um eine Überflutung des Datenträgersubsystems zu vermeiden.| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_DBSTARTUP |Tritt beim Datenbankstart auf, während darauf gewartet wird, dass alle Datenbanken wiederhergestellt werden.| 
|SLEEP_DCOMSTARTUP |Tritt einmal auf höchstens während des Starts von SQL Server-Instanz während des Wartens auf DCOM-Initialisierung.| 
|SLEEP_MASTERDBREADY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERMDREADY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERUPGRADED |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MSDBSTARTUP |Tritt auf, wenn die SQL-Ablaufverfolgung auf den Abschluss des Startvorgangs der msdb-Datenbank wartet.| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_SYSTEMTASK |Tritt beim Start eines Hintergrundtasks auf, während auf den Abschluss des Startvorgangs von tempdb gewartet wird.| 
|SLEEP_TASK |Tritt auf, wenn ein Task ruht, während auf das Auftreten eines generischen Ereignisses gewartet wird.| 
|SLEEP_TEMPDBSTARTUP |Tritt auf, während ein Task auf den Abschluss des Startvorgangs von tempdb wartet.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLO_UPDATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SMSYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CONN_DUP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CRITICAL_SECTION |Tritt auf, während der internen Synchronisierung innerhalb von SQL Server-Netzwerkkomponenten.| 
|SNI_HTTP_WAITFOR_0_DISCON |Tritt auf, während SQL Server wird heruntergefahren, während des Wartens auf ausstehender HTTP-Verbindungen beendet.| 
|SNI_LISTENER_ACCESS |Tritt auf, während darauf gewartet wird, dass nicht einheitliche Speicherzugriffsknoten (Non-Uniform Memory Access, NUMA) die Statusänderung aktualisieren. Der Zugriff auf die Statusänderung wird serialisiert.| 
|SNI_TASK_COMPLETION |Tritt bei einem Wartevorgang auf das Beenden aller Tasks während der Statusänderung eines NUMA-Knotens auf.| 
|SNI_WRITE_ASYNC |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOAP_READ |Tritt während eines Wartevorgangs auf den Abschluss eines HTTP-Netzwerklesevorgangs auf.| 
|SOAP_WRITE |Tritt auf, während auf den Abschluss eines HTTP-Netzwerkschreibvorgangs gewartet wird.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_CALLBACK_REMOVAL |Tritt beim Ausführen einer Synchronisierung für eine Rückrufliste auf, um einen Rückruf zu entfernen. Es wird nicht erwartet, dass dieser Leistungsindikator nach dem Abschluss der Serverinitialisierung geändert wird.| 
|SOS_DISPATCHER_MUTEX |Tritt während der internen Synchronisierung des Verteilerpools auf. Dies schließt Anpassungsvorgänge des Pools mit ein.| 
|SOS_LOCALALLOCATORLIST |Tritt auf, während der internen Synchronisierung in der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Speicher-Manager. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_MEMORY_USAGE_ADJUSTMENT |Tritt auf, wenn die Speicherauslastung zwischen Pools angepasst wird.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |Tritt während der internen Synchronisierung in Speicherpools auf, wenn Objekte im Pool gelöscht werden.| 
|SOS_PHYS_PAGE_CACHE |Bezieht sich auf die Zeit, die ein Thread beim Abrufen des Mutex wartet, das erforderlich ist, bevor physische Seiten zugeordnet oder diese Seiten an das Betriebssystem zurückgegeben werden. Wartevorgänge für diesen Typ wird nur angezeigt, wenn der SQL Server-Instanz AWE-Arbeitsspeicher nutzt., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_PROCESS_AFFINITY_MUTEX |Tritt während der Synchronisierung des Zugriffs für die Verarbeitung von Affinitätseinstellungen auf.| 
|SOS_RESERVEDMEMBLOCKLIST |Tritt auf, während der internen Synchronisierung in der SQL Server-Speicher-Manager. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|SOS_SCHEDULER_YIELD |Tritt auf, wenn ein Task freiwillig das Zeitplanungsmodul freigibt, damit andere Tasks ausgeführt werden können. Während dieses Wartevorgangs wartet der Task darauf, dass sein Quantum erneuert wird.| 
|SOS_SMALL_PAGE_ALLOC |Tritt während der Zuordnung und Freigabe von Arbeitsspeicher auf, der von einigen Arbeitsspeicherobjekten verwaltet wird.| 
|SOS_STACKSTORE_INIT_MUTEX |Tritt während der Synchronisierung der Initialisierung des internen Speichers auf.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |Tritt auf, wenn ein Task synchron gestartet wird. Die meisten Tasks in SQL Server werden auf asynchrone Weise gestartet, die Steuerung zum Starter zurück sofort, nachdem die taskanforderung in der Arbeitswarteschlange angeordnet wurde.| 
|SOS_VIRTUALMEMORY_LOW |Tritt auf, wenn eine Speicherbelegung darauf wartet, dass ein Ressourcen-Manager virtuellen Arbeitsspeicher freigibt.| 
|SOSHOST_EVENT |Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf ein Synchronisierungsobjekt für SQL Server-Ereignis wartet.| 
|SOSHOST_INTERNAL |Tritt während der Synchronisierung von Rückrufen des Speicher-Managers auf, die von gehosteten Komponenten, wie z. B. CLR, verwendet werden.| 
|SOSHOST_MUTEX |Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf ein mutexsynchronisierungsobjekt von SQL Server wartet.| 
|SOSHOST_RWLOCK |Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf ein SQL Server Leser-Synchronisierungsobjekt wartet.| 
|SOSHOST_SEMAPHORE |Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf ein semaphorensynchronisierungsobjekt von SQL Server wartet.| 
|SOSHOST_SLEEP |Tritt auf, wenn ein gehosteter Task ruht, während auf das Auftreten eines generischen Ereignisses gewartet wird. Gehostete Tasks werden von gehosteten Komponenten, wie z. B. CLR, verwendet.| 
|SOSHOST_TRACELOCK |Tritt während der Synchronisierung des Zugriffs auf Ablaufverfolgungsdatenströme auf.| 
|SOSHOST_WAITFORDONE |Tritt auf, wenn eine gehostete Komponente, wie z. B. CLR, auf den Abschluss eines Tasks wartet.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLCLR_APPDOMAIN |Tritt auf, während CLR auf den Abschluss des Startvorgangs einer Anwendungsdomäne wartet.| 
|SQLCLR_ASSEMBLY |Tritt auf, während auf den Zugriff auf die Liste der geladenen Assemblys in der Anwendungsdomäne gewartet wird.| 
|SQLCLR_DEADLOCK_DETECTION |Tritt auf, während CLR auf den Abschluss der Deadlockerkennung wartet.| 
|SQLCLR_QUANTUM_PUNISHMENT |Tritt auf, wenn ein CLR-Task gedrosselt wird, weil er sein Ausführungsquantum überschritten hat. Diese Drosselung wird ausgeführt, um die Auswirkungen dieses ressourcenintensiven Tasks auf andere Tasks zu reduzieren.| 
|SQLSORT_NORMMUTEX |Tritt bei der internen Synchronisierung auf, während interne Sortierungsstrukturen initialisiert werden.| 
|SQLSORT_SORTMUTEX |Tritt bei der internen Synchronisierung auf, während interne Sortierungsstrukturen initialisiert werden.| 
|SQLTRACE_BUFFER_FLUSH |Tritt auf, wenn ein Task darauf wartet, dass ein Hintergrundtask Ablaufverfolgungspuffer alle vier Sekunden auf den Datenträger leert. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|SQLTRACE_FILE_BUFFER |Tritt während der Synchronisierung für Ablaufverfolgungspuffer während einer dateiablaufverfolgung., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_LOCK |TBD <br /> **GILT für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_SHUTDOWN |Tritt auf, während das Herunterfahren der Ablaufverfolgung auf den Abschluss ausstehender Ablaufverfolgungsereignisse wartet.| 
|SQLTRACE_WAIT_ENTRIES |Tritt auf, während eine Ereigniswarteschlange der SQL-Ablaufverfolgung auf das Eintreffen von Paketen in der Warteschlange wartet.| 
|SRVPROC_SHUTDOWN |Tritt auf, während der Prozess des Herunterfahrens auf die Freigabe interner Ressourcen wartet, damit ein ordnungsgemäßes Herunterfahren erfolgen kann.| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_BANDWIDTH_STATE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_INIT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_PROXY_CONTAINER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TEMPOBJ |Tritt auf, wenn Löschvorgänge temporärer Objekte synchronisiert werden. Dieser Wartetyp ist selten und tritt nur auf, wenn ein Task einen exklusiven Zugriff für temp-Tabellenlöschvorgänge angefordert hat.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TERMINATE_LISTENER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|THREADPOOL |Tritt auf, wenn ein Task auf die weitere Ausführung eines Arbeitsthreads wartet. Dies kann anzeigen, dass die Einstellung für die maximale Anzahl von Arbeitsthreads zu niedrig ist oder die Ausführung von Batches ungewöhnlich lange dauert, wodurch die Anzahl der Arbeitsthreads reduziert wird, die für das Ausführen anderer Batches verfügbar sind.| 
|TIMEPRIV_TIMEPERIOD |Tritt während der internen Synchronisierung des Zeitgebers für erweiterte Ereignisse auf.| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |Tritt auf, wenn der Rowset-Ablaufverfolgungsanbieter der SQL-Ablaufverfolgung entweder auf einen freien Puffer oder auf einen Puffer mit zu verarbeitenden Ereignissen wartet.| 
|TRAN_MARKLATCH_DT |Tritt auf, wenn auf einen Latch im Löschmodus für einen Transaktionsmarkierungslatch gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.| 
|TRAN_MARKLATCH_EX |Tritt auf, wenn auf einen Latch im exklusiven Modus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.| 
|TRAN_MARKLATCH_KP |Tritt auf, wenn auf einen Latch im Beibehaltungsmodus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.| 
|TRAN_MARKLATCH_NL |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|TRAN_MARKLATCH_SH |Tritt auf, wenn auf einen Latch im freigegebenen Modus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.| 
|TRAN_MARKLATCH_UP |Tritt auf, wenn auf einen Latch im Updatemodus für eine markierte Transaktion gewartet wird. Transaktionsmarkierungslatches werden für die Synchronisierung von Commit-Vorgängen mit markierten Transaktionen verwendet.| 
|TRANSACTION_MUTEX |Tritt während der Synchronisierung des Zugriffs auf eine Transaktion durch mehrere Batches auf.| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MANAGER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_SESSION_REGISTRATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UTIL_PAGE_ALLOC |Tritt auf, wenn Transaktionsprotokollscans darauf warten, dass Arbeitsspeicher bei unzureichendem Arbeitsspeicher verfügbar ist.| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OPERATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OTHER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VERSIONING_COMMITTING |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VIA_ACCEPT |Tritt auf, wenn eine VIA (Virtual Interface Adapter)-Anbieterverbindung während des Startvorgangs abgeschlossen wird.| 
|VIEW_DEFINITION_MUTEX |Tritt während der Synchronisierung für den Zugriff auf zwischengespeicherte Sichtdefinitionen auf.| 
|WAIT_FOR_RESULTS |Tritt auf, wenn auf das Auslösen einer Abfragebenachrichtigung gewartet wird.| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_CLOSE |Tritt beim Warten auf Abschluss eines Prüfpunkts., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_ENABLED |Tritt auf, wenn die prüfpunktausführung deaktiviert ist, und Warten auf die prüfpunktausführung aktiviert ist., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_STATE_LOCK |Tritt beim Synchronisieren der Überprüfung des prüfpunktstatus., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **GILT FÜR:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]| 
|WAIT_XTP_GUEST |Tritt auf, wenn die datenbankspeicherbelegung den Empfang von Benachrichtigungen Arbeitsspeicherstatus niedrig zu halten., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_HOST_WAIT |Tritt auf, wenn Wartevorgänge vom Datenbankmodul ausgelöst und vom Host implementiert werden., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |Tritt auf, wenn der offline-Prüfpunkt wartet ein Protokoll e/a, abgeschlossen lesen., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |Tritt auf, wenn der offline-Prüfpunkt Scannen neue Protokolldatensätze wartet., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_PROCEDURE_ENTRY |Tritt auf, wenn ein Drop-Verfahren darauf wartet, dass alle aktuellen Ausführungen dieser Prozedur abgeschlossen werden., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_RECOVERY |Tritt auf, wenn die Wiederherstellung der Datenbank für die Wiederherstellung von speicheroptimierten Objekten abgeschlossen wartet., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TASK_SHUTDOWN |Tritt beim Warten auf eines In-Memory-OLTP-Threads abgeschlossen., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TRAN_DEPENDENCY |Tritt auf, wenn auf transaktionsabhängigkeiten gewartet wird., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR |Als Ergebnis einer WAITFOR Transact-SQL-Anweisung auftritt. Die Dauer des Wartevorgangs wird durch die Parameter der Anweisung bestimmt. Hierbei handelt es sich um einen vom Benutzer initiierten Wartevorgang.| 
|WAITFOR_PER_QUEUE |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR_TASKSHUTDOWN |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|WAITSTAT_MUTEX |Tritt während der Synchronisierung des Zugriffs auf die Statistikauflistung auf, die zum Auffüllen von sys.dm_os_wait_stats verwendet wird.| 
|WCC |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_API_CALL |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPORT_FAULT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WORKTBL_DROP |Tritt während des Anhaltens vor einem erneuten Versuch nach einem fehlerhaften Löschvorgang einer Arbeitstabelle auf.| 
|WRITE_COMPLETION |Tritt während der Ausführung eines Schreibvorgangs auf.| 
|WRITELOG |Tritt auf, während auf den Abschluss einer Protokollleerung gewartet wird. Häufig verwendete Vorgänge, die Protokollleerungen verursachen, sind Prüfpunkte und Transaktionscommits.| 
|XACT_OWN_TRANSACTION |Tritt auf, während auf das Abrufen des Besitzes einer Transaktion gewartet wird.| 
|XACT_RECLAIM_SESSION |Tritt auf, während darauf gewartet wird, dass der aktuelle Besitzer einer Sitzung den Besitz der Sitzung freigibt.| 
|XACTLOCKINFO |Tritt während der Synchronisierung des Zugriffs auf die Liste von Sperren für eine Transaktion auf. Zusätzlich zur Transaktion selbst erfolgt der Zugriff auf die Liste von Sperren durch Vorgänge, wie z. B. Deadlockerkennung und Sperrenmigration, während Seitenteilungen.| 
|XACTWORKSPACE_MUTEX |Tritt während der Synchronisierung von Austritten aus einer Transaktion sowie der Anzahl von Datenbanksperren zwischen eingetragenen Mitgliedern einer Transaktion auf.| 
|XDB_CONN_DUP_HASH |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_HISTORY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_SNAPSHOT |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDESTSVERMGR |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |Tritt auf, wenn Puffer einer Sitzung für erweiterte Ereignisse an Ziele gesendet werden. Dieser Wartetyp tritt in einem Hintergrundthread auf.| 
|XE_BUFFERMGR_FREEBUF_EVENT |Tritt auf, wenn eine der folgenden Bedingungen zutrifft:| 
|XE_CALLBACK_LIST |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_CX_FILE_READ |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |Tritt auf, wenn eine Sitzung für erweiterte Ereignisse, die asynchrone Ziele verwendet, begonnen oder beendet wird. Dieser Wartetyp weist auf eines der folgenden Ereignisse hin:| 
|XE_DISPATCHER_JOIN |Tritt auf, wenn ein für Sitzungen für erweiterte Ereignisse verwendeter Hintergrundthread beendet wird.| 
|XE_DISPATCHER_WAIT |Tritt auf, wenn ein für Sitzungen für erweiterte Ereignisse verwendeter Hintergrundthread auf die Verarbeitung von Ereignispuffern wartet.| 
|XE_FILE_TARGET_TVF |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_LIVE_TARGET_TVF |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_MODULEMGR_SYNC |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|XE_OLS_LOCK |Nur für Informationszwecke identifiziert. Wird nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.| 
|XE_PACKAGE_LOCK_BACKOFF |Nur für Informationszwecke identifiziert. Nicht unterstützt. <br /> **Gilt für**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] nur. |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_TRUNCATION_LSN |TBD <br /> **Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_CACHE_ACCESS |Tritt auf, wenn für den Zugriff auf alle Cacheobjekte der systemintern kompilierten gespeicherten Prozedur., <br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_PARTITIONED_STACK_CREATE |Tritt auf, wenn das Zuordnen von pro NUMA-Knoten systemintern gespeicherte Prozedur Cache Strukturen (muss erfolgen, Singlethread) für eine angegebene Prozedur kompiliert., <br /> **Gilt für**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|

  
 Die folgenden XEvents beziehen sich auf Partition **SWITCH** und Neuerstellung von Onlineindizes. Weitere Informationen zur Syntax finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) und [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Einer der sperrenkompatibilität finden Sie unter [Sys. dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
    
 [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Sys. dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [Sys. dm_db_wait_stats &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


