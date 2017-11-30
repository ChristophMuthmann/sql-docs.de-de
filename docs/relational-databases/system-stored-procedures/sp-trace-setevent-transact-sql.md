---
title: Sp_trace_setevent (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_trace_setevent_TSQL
- sp_trace_setevent
dev_langs: TSQL
helpviewer_keywords: sp_trace_setevent
ms.assetid: 7662d1d9-6d0f-443a-b011-c901a8b77a44
caps.latest.revision: "49"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f47656c08b4cdf835a9f7d6dc7e9ae0b84dbdca9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sptracesetevent-transact-sql"></a>sp_trace_setevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einer Ablaufverfolgung ein Ereignis oder eine Ereignisspalte hinzu oder entfernt diese(s). **Sp_trace_setevent** möglicherweise nur für vorhandene beendete ablaufverfolgungen ausgeführt (*Status* ist **0**). Ein Fehler wird zurückgegeben, wenn diese gespeicherte Prozedur wird ausgeführt, auf eine Ablaufverfolgung, die nicht vorhanden ist oder deren *Status* nicht **0**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_trace_setevent [ @traceid = ] trace_id   
          , [ @eventid = ] event_id  
          , [ @columnid = ] column_id  
          , [ @on = ] on  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@traceid=** ] *Trace_id*  
 Die ID der zu ändernden Ablaufverfolgung. *Trace_id* ist **Int**, hat keinen Standardwert. Der Benutzer verwendet diesen *Trace_id* Wert zum Identifizieren, ändern und Steuern der Ablaufverfolgung.  
  
 [  **@eventid=** ] *"event_id"*  
 Die ID des Ereignisses, das aktiviert werden soll. *event_id* ist vom Datentyp **int**und hat keinen Standardwert.  
  
 Die folgende Tabelle führt die Ereignisse auf, die zu einer Ablaufverfolgung hinzugefügt bzw. aus ihr entfernt werden können.  
  
|Ereignisnummer|Ereignisname|Description|  
|------------------|----------------|-----------------|  
|0-9|Reserviert.|Reserviert.|  
|10|RPC:Completed|Tritt auf, wenn ein Remoteprozeduraufruf (RPC, Remote Procedure Call) abgeschlossen wurde.|  
|11|RPC:Starting|Tritt auf, wenn ein RPC gestartet wurde.|  
|12|SQL:BatchCompleted|Tritt auf, wenn ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch abgeschlossen wurde.|  
|13|SQL:BatchStarting|Tritt auf, wenn ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch gestartet wurde.|  
|14|Audit Login|Tritt auf, wenn sich ein Benutzer erfolgreich an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anmeldet.|  
|15|Audit Logout|Tritt auf, wenn sich ein Benutzer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abmeldet.|  
|16|Attention|Tritt auf, wenn Anforderungsereignisse auftreten, wie z. B. Clientunterbrechungsanforderungen oder das Unterbrechen von Clientverbindungen.|  
|17|ExistingConnection|Erkennt alle Aktivitäten von Benutzern, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden waren, bevor die Ablaufverfolgung gestartet wurde.|  
|18|Audit Server Starts and Stops|Tritt auf, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienststatus geändert wird.|  
|19|DTCTransaction|Verfolgt von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) koordinierte Transaktionen zwischen zwei oder mehr Datenbanken nach.|  
|20|Audit Login Failed|Zeigt an, dass beim Anmeldeversuch an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch einen Client ein Fehler aufgetreten ist.|  
|21|EventLog|Zeigt an, dass Ereignisse im Windows-Anwendungsprotokoll protokolliert wurden.|  
|22|ErrorLog|Zeigt an, dass Fehlerereignisse im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll protokolliert wurden.|  
|23|Lock:Released|Kennzeichnet, dass eine Sperre auf einer Ressource, wie z. B. einer Seite, freigegeben wurde.|  
|24|Lock:Acquired|Kennzeichnet den Erhalt einer Sperre auf einer Ressource, z. B. einer Datenseite.|  
|25|Lock:Deadlock|Kennzeichnet, dass sich zwei gleichzeitige Transaktionen gegenseitig blockiert haben, indem sie versucht haben, inkompatible Sperren auf Ressourcen zu erhalten, die sich im Besitz der jeweils anderen Transaktion befinden.|  
|26|Lock:Cancel|Kennzeichnet, dass der Erhalt einer Sperre auf einer Ressource abgebrochen wurde (z. B. aufgrund eines Deadlocks).|  
|27|Lock:Timeout|Kennzeichnet, dass für die Anforderung für eine Sperre auf einer Ressource, wie z. B. einer Seite, ein Timeout aufgetreten ist, da eine andere Transaktion eine blockierende Sperre für die angeforderte Ressource aufrechterhält. Timeout richtet sich nach der @@LOCK_TIMEOUT -Funktion und kann durch die SET LOCK_TIMEOUT-Anweisung festgelegt werden.|  
|28|Degree of Parallelism-Ereignis (7.0 Insert)|Tritt auf, bevor eine SELECT-, INSERT- oder UPDATE-Anweisung ausgeführt wird.|  
|29-31|Reserviert.|Verwenden Sie stattdessen das Ereignis 28.|  
|32|Reserviert.|Reserviert.|  
|33|Exception|Zeigt an, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Ausnahme aufgetreten ist.|  
|34|SP:CacheMiss|Zeigt an, dass eine gespeicherte Prozedur nicht im Prozedurcache gefunden wurde.|  
|35|SP:CacheInsert|Zeigt an, dass ein Element in den Prozedurcache eingefügt wurde.|  
|36|SP:CacheRemove|Zeigt an, dass ein Element aus dem Prozedurcache entfernt wurde.|  
|37|SP:Recompile|Zeigt an, dass eine gespeicherte Prozedur neu kompiliert wurde.|  
|38|SP:CacheHit|Zeigt an, dass eine gespeicherte Prozedur im Prozedurcache gefunden wurde.|  
|39|Als veraltet markiert|Als veraltet markiert|  
|40|SQL:StmtStarting|Tritt auf, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung gestartet wurde.|  
|41|SQL:StmtCompleted|Tritt auf, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung abgeschlossen wurde.|  
|42|SP:Starting|Zeigt an, dass eine gespeicherte Prozedur gestartet wurde.|  
|43|SP:Completed|Zeigt an, dass eine gespeicherte Prozedur abgeschlossen wurde.|  
|44|SP:StmtStarting|Zeigt an, dass die Ausführung einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung in einer gespeicherten Prozedur gestartet wurde.|  
|45|SP:StmtCompleted|Zeigt an, dass die Ausführung einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung in einer gespeicherten Prozedur abgeschlossen wurde.|  
|46|Object:Created|Zeigt an, dass ein Objekt erstellt wurde, z. B. durch eine CREATE INDEX-, CREATE TABLE- oder CREATE DATABASE-Anweisung.|  
|47|Object:Deleted|Zeigt an, dass ein Objekt gelöscht wurde, z. B. durch eine DROP INDEX- oder DROP TABLE-Anweisung.|  
|48|Reserviert.||  
|49|Reserviert.||  
|50|SQL Transaction|Verfolgt die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen BEGIN, COMMIT, SAVE und ROLLBACK TRANSACTION nach.|  
|51|Scan:Started|Zeigt an, dass ein Tabellen- oder Indexscan gestartet wurde.|  
|52|Scan:Stopped|Zeigt an, dass ein Tabellen- oder Indexscan beendet wurde.|  
|53|CursorOpen|Zeigt an, dass ein Cursor für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung durch ODBC, OLE DB oder DB-Library.geöffnet wird.|  
|54|TransactionLog|Verfolgt nach, wenn Transaktionen in das Transaktionsprotokoll geschrieben werden.|  
|55|Hash Warning|Zeigt an, dass ein Hashvorgang (z. B. Hashjoin, Hashaggregat, Hashvereinigung, Hash-Distinct), der nicht auf einer Pufferpartition durchgeführt wird, nach einem Alternativplan durchgeführt wird. Dies kann aufgrund der Rekursionstiefe, einer Datendrehung (data skew), der Ablaufverfolgungsflags oder der Bitzählung vorkommen.|  
|56-57|Reserviert.||  
|58|Auto Stats|Zeigt an, dass ein automatisches Update der Indexstatistiken aufgetreten ist.|  
|59|Lock:Deadlock Chain|Wird für jedes der Ereignisse erstellt, die zu dem Deadlock führen.|  
|60|Lock:Escalation|Zeigt an, dass eine differenziertere Sperre in eine gröbere Sperre konvertiert wurde (z. B. eine Seitensperre wurde zu einer TABLE- oder HoBT-Sperre ausgeweitet oder in eine solche konvertiert).|  
|61|OLE DB Errors|Zeigt einen OLE DB-Fehler an.|  
|62-66|Reserviert.||  
|67|Execution Warnings|Zeigt alle Warnungen an, die während der Ausführung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anweisung oder einer gespeicherten Prozedur aufgetreten sind.|  
|68|Showplan Text (Unencoded)|Zeigt die Planstruktur der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung an, die gerade ausgeführt wird.|  
|69|Sort Warnings|Zeigt Sortiervorgänge an, für die der Arbeitsspeicher nicht ausreicht. Sortiervorgänge, die die Indexerstellung beinhalten, sind nicht eingeschlossen, sondern nur Sortiervorgänge mit einer Abfrage (z. B. eine ORDER BY-Klausel in einer SELECT-Anweisung).|  
|70|CursorPrepare|Zeigt an, wenn die Verwendung eines Cursors für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung durch ODBC, OLE DB oder DB-Library vorbereitet wird.|  
|71|Prepare SQL|ODBC, OLE DB oder DB-Library hat mindestens eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung für die Verwendung vorbereitet.|  
|72|Exec Prepared SQL|ODBC, OLE DB oder DB-Library hat mindestens eine vorbereitete [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ausgeführt.|  
|73|Unprepare SQL|ODBC, OLE DB oder DB-Library hat die Vorbereitung mindestens einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aufgehoben (gelöscht).|  
|74|CursorExecute|Ein Cursor, der zuvor für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung durch ODBC, OLE DB oder DB-Library vorbereitet wurde, wird ausgeführt.|  
|75|CursorRecompile|Ein für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung durch ODBC oder DB-Library geöffneter Cursor wurde entweder direkt oder aufgrund einer Schemaänderung neu kompiliert.<br /><br /> Wird für ANSI- sowie Nicht-ANSI-Cursor ausgelöst.|  
|76|CursorImplicitConversion|Ein Cursor für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem Typ in einen anderen Typ konvertiert.<br /><br /> Wird für ANSI- sowie Nicht-ANSI-Cursor ausgelöst.|  
|77|CursorUnprepare|Die Vorbereitung eines Cursors für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung wurde durch ODBC, OLE DB oder DB-Library aufgehoben (gelöscht).|  
|78|CursorClose|Ein Cursor, der zuvor für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung durch ODBC, OLE DB oder DB-Library geöffnet wurde, wird geschlossen.|  
|79|Missing Column Statistics|Spaltenstatistiken, die vom Optimierer hätten verwendet werden können, sind nicht verfügbar.|  
|80|Missing Join Predicate|Eine Abfrage wird ausgeführt, die kein Joinprädikat aufweist. Dies kann zu einer langen Ausführungszeit für die Abfrage führen.|  
|81|Server Memory Change|Die Speicherauslastung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist über 1 MB oder 5 % des maximal zulässigen Serverarbeitsspeichers (je nachdem, welcher Wert größer ist) gestiegen bzw. gesunken.|  
|82-91|Vom Benutzer konfigurierbar (0 -9)|Vom Benutzer definierte Ereignisdaten.|  
|92|Data File Auto Grow|Gibt an, dass eine Datendatei automatisch vom Server erweitert wurde.|  
|93|Log File Auto Grow|Zeigt an, dass eine Protokolldatei automatisch vom Server erweitert wurde.|  
|94|Data File Auto Shrink|Zeigt an, dass eine Datendatei automatisch vom Server verkleinert wurde.|  
|95|Log File Auto Shrink|Zeigt an, dass eine Protokolldatei automatisch vom Server verkleinert wurde.|  
|96|Showplan Text|Zeigt die Abfrageplanstruktur des Abfrageoptimierers für die SQL-Anweisung an. Beachten Sie, dass die **TextData** Spalte enthält den Showplan für dieses Ereignis nicht.|  
|97|Showplan All|Zeigt den Abfrageplan mit vollständigen Kompilierzeitinformationen für die SQL-Anweisung an, die gerade ausgeführt wird. Beachten Sie, dass die **TextData** Spalte enthält den Showplan für dieses Ereignis nicht.|  
|98|Showplan Statistics Profile|Zeigt den Abfrageplan mit vollständigen Laufzeitinformationen für die SQL-Anweisung an, die gerade ausgeführt wird. Beachten Sie, dass die **TextData** Spalte enthält den Showplan für dieses Ereignis nicht.|  
|99|Reserviert.||  
|100|RPC Output Parameter|Erzeugt Ausgabewerte der Parameter für jeden RPC.|  
|101|Reserviert.||  
|102|Audit Database Scope GDR|Wird immer dann ausgelöst, wenn ein Benutzer in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine GRANT-, REVOKE- oder DENY-Anweisung für eine Anweisungsberechtigung ausgibt (dies gilt ausschließlich für datenbankspezifische Ereignisse, beispielsweise das Gewähren von Berechtigungen für eine Datenbank).|  
|103|Audit Object GDR Event|Tritt jedes Mal dann auf, wenn GRANT, DENY oder REVOKE für eine Objektberechtigung von einem Benutzer in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingegeben wird.|  
|104|Audit AddLogin Event|Tritt auf, wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung hinzugefügt oder entfernt wurde, wird für **Sp_addlogin** und **Sp_droplogin**.|  
|105|Audit Login GDR Event|Tritt auf, wenn ein Windows-Anmelderecht hinzugefügt oder entfernt wird; für **Sp_grantlogin**, **Sp_revokelogin**, und **Sp_denylogin**.|  
|106|Audit Login Change Property Event|Tritt auf, wenn eine Eigenschaft eines Anmeldenamens, außer Kennwörtern, geändert wird. für **Sp_defaultdb** und **Sp_defaultlanguage**.|  
|107|Audit Login Change Password Event|Tritt auf, wenn das Kennwort für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen geändert wird.<br /><br /> Kennwörter werden nicht aufgezeichnet.|  
|108|Audit Add Login to Server Role Event|Tritt auf, wenn eine Anmeldung hinzugefügt oder aus einer festen Serverrolle entfernt wird; für **Sp_addsrvrolemember**, und **Sp_dropsrvrolemember**.|  
|109|Audit Add DB User Event|Tritt auf, wenn eine Anmeldung hinzugefügt oder werden, wie ein Datenbankbenutzer entfernt (Windows oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) in einer Datenbank; für **Sp_grantdbaccess**, **Sp_revokedbaccess**, **Sp_adduser**, und **Sp_dropuser**.|  
|110|Audit Add Member to DB Role Event|Tritt auf, wenn eine Anmeldung hinzugefügt oder, da ein Datenbankbenutzer entfernt (fest oder benutzerdefinierte) in einer Datenbank. für **Sp_addrolemember**, **Sp_droprolemember**, und **Sp_changegroup**.|  
|111|Audit Add Role Event|Tritt auf, wenn eine Anmeldung hinzugefügt oder, da ein Datenbankbenutzer zu einer Datenbank entfernt. für **Sp_addrole** und **Sp_droprole**.|  
|112|Audit App Role Change Password Event|Tritt auf, wenn ein Kennwort für eine Anwendungsrolle geändert wird.|  
|113|Audit Statement Permission Event|Tritt auf, wenn eine Anweisungsberechtigung, wie z. B. CREATE TABLE, verwendet wird.|  
|114|Audit Schema Object Access Event|Tritt auf, wenn eine Objektberechtigung, wie z. B. SELECT, verwendet wird, unabhängig vom Erfolg.|  
|115|Audit Backup/Restore Event|Tritt auf, wenn ein BACKUP- oder RESTORE-Befehl ausgegeben wird.|  
|116|Audit DBCC Event|Tritt auf, wenn DBCC-Befehle ausgegeben werden.|  
|117|Audit Change Audit Event|Tritt auf, wenn Änderungen an der Überwachung für die Ablaufverfolgung vorgenommen werden.|  
|118|Audit Object Derived Permission Event|Tritt auf, wenn CREATE-, ALTER- und DROP-Objektbefehle ausgegeben werden.|  
|119|OLEDB Call Event|Tritt auf, wenn für verteilte Abfragen und remote gespeicherte Prozeduren Aufrufe des OLE DB-Anbieters ausgegeben werden.|  
|120|OLEDB QueryInterface Event|Tritt auf, wenn OLE DB **QueryInterface** Aufrufe für verteilte Abfragen und remote gespeicherte Prozeduren.|  
|121|OLEDB DataRead Event|Tritt auf, wenn ein Datenanforderungsaufruf an den OLE DB-Anbieter ausgegeben wird.|  
|122|Showplan XML|Tritt auf, wenn eine SQL-Anweisung ausgeführt wird. Schließen Sie dieses Ereignis mit ein, um Showplanoperatoren anzugeben. Jedes Ereignis wird in einem wohlgeformten XML-Dokument gespeichert. Beachten Sie, dass die **binäre** Spalte für dieses Ereignis den codierten Showplan enthält. Verwenden Sie SQL Server Profiler, um die Ablaufverfolgung zu öffnen und den Showplan anzuzeigen.|  
|123|SQL:FullTextQuery|Tritt auf, wenn eine Volltextabfrage ausgeführt wird.|  
|124|Broker:Conversation|Meldet den Fortschritt einer [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Konversation.|  
|125|Deprecation Announcement|Tritt auf, wenn Sie eine Funktion verwenden, die aus einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt wird.|  
|126|Deprecation Final Support|Tritt auf, wenn Sie eine Funktion verwenden, die aus der nächsten Hauptversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt wird.|  
|127|Exchange Spill Event|Tritt auf, wenn Kommunikationspuffer in einem parallelen Abfrageplan vorübergehend in das geschrieben wurden die **Tempdb** Datenbank.|  
|128|Audit Database Management Event|Tritt auf, wenn eine Datenbank erstellt, geändert oder gelöscht wird.|  
|129|Audit Database Object Management Event|Tritt auf, wenn eine CREATE-, ALTER- oder DROP-Anweisung für Datenbankobjekte, wie z. B. Schemas, ausgeführt wird.|  
|130|Audit Database Principal Management Event|Tritt auf, wenn Prinzipale, wie z. B. Benutzer, in einer Datenbank erstellt oder geändert bzw. aus einer Datenbank gelöscht werden.|  
|131|Audit Schema Object Management Event|Tritt auf, wenn Serverobjekte erstellt, geändert oder gelöscht werden.|  
|132|Audit Server Principal Impersonation Event|Tritt auf, wenn es einen Identitätswechsel im Serverbereich gibt, wie z. B. bei EXECUTE AS LOGIN.|  
|133|Audit Database Principal Impersonation Event|Tritt auf, wenn im Datenbankbereich ein Identitätswechsel auftritt, wie z. B. EXECUTE AS USER oder SETUSER.|  
|134|Audit Server Object Take Ownership Event|Tritt auf, wenn im Serverbereich der Besitzer für Objekte geändert wird.|  
|135|Audit Database Object Take Ownership Event|Tritt auf, wenn im Datenbankbereich der Besitzer für Objekte geändert wird.|  
|136|Broker:Conversation Group|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine neue Konversationsgruppe erstellt oder eine vorhandene Konversationsgruppe gelöscht wird.|  
|137|Blocked Process Report|Tritt auf, wenn ein Prozess länger als einen festgelegten Zeitraum blockiert ist. Schließt keine Systemprozesse oder Prozesse ein, die auf Ressourcen warten, für die keine Deadlocks erkannt werden können. Verwendung **Sp_configure** so konfigurieren Sie den Schwellenwert und die Häufigkeit der berichtgenerierung.|  
|138|Broker:Connection|Gibt den Status einer Transportverbindung an, die von [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwaltet wird.|  
|139|Broker:Forwarded Message Sent|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Nachricht weitergeleitet wird.|  
|140|Broker:Forwarded Message Dropped|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Nachricht gelöscht wird, die weitergeleitet werden sollte.|  
|141|Broker:Message Classify|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] das Routing für eine Nachricht bestimmt wird.|  
|142|Broker:Transmission|Zeigt an, dass auf der Transportebene von [!INCLUDE[ssSB](../../includes/sssb-md.md)] Fehler aufgetreten sind. Die Fehlernummer und Statuswerte kennzeichnen die Fehlerquelle.|  
|143|Broker:Queue Disabled|Zeigt an, dass eine beschädigte Nachricht erkannt wurde, weil in einer [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Warteschlange fünf Transaktionsrollbacks aufeinander folgten. Das Ereignis enthält die Datenbank-ID und die Warteschlangen-ID der Warteschlange mit der beschädigten Nachricht.|  
|144-145|Reserviert.||  
|146|Showplan XML Statistics Profile|Tritt auf, wenn eine SQL-Anweisung ausgeführt wird. Identifiziert die Showplanoperatoren und zeigt vollständige Kompilierzeitdaten an. Beachten Sie, dass die **binäre** Spalte für dieses Ereignis den codierten Showplan enthält. Verwenden Sie SQL Server Profiler, um die Ablaufverfolgung zu öffnen und den Showplan anzuzeigen.|  
|148|Deadlock Graph|Tritt auf, wenn der Versuch, eine Sperre zu aktivieren, abgebrochen wird, da der Versuch Teil eines Deadlocks war und als Deadlockopfer ausgewählt wurde. Stellt eine XML-Beschreibung eines Deadlocks bereit.|  
|149|Broker:Remote Message Acknowledgement|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Nachrichtenbestätigung gesendet oder empfangen wird.|  
|150|Trace File Close|Tritt auf, wenn eine Ablaufverfolgungsdatei beim Rollover für Ablaufverfolgungsdateien geschlossen wird.|  
|151|Reserviert.||  
|152|Audit Change Database Owner|Tritt auf, wenn ALTER AUTHORIZATION verwendet wird, um den Besitzer einer Datenbank zu ändern, und die entsprechenden Berechtigungen geprüft werden.|  
|153|Audit Schema Object Take Ownership Event|Tritt auf, wenn ALTER AUTHORIZATION verwendet wird, um einem Objekt einen Besitzer zuzuweisen, und die Berechtigungen dafür geprüft werden.|  
|154|Reserviert.||  
|155|FT:Crawl Started|Tritt auf, wenn eine Volltextdurchforstung (Auffüllung) gestartet wird. Wird verwendet, um zu prüfen, ob eine Durchforstungsanforderung von Arbeitstasks abgerufen wird.|  
|156|FT:Crawl Stopped|Tritt auf, wenn eine Volltextdurchforstung (Auffüllung) beendet wird. Die Beendigung kann bei einem erfolgreichen Abschließen des Durchforstungsvorgangs oder bei einem schwerwiegenden Fehler erfolgen.|  
|157|FT:Crawl Aborted|Tritt auf, wenn bei einer Volltextdurchforstung eine Ausnahme festgestellt wird. In der Regel wird die Volltextdurchforstung dadurch angehalten.|  
|158|Audit Broker Conversation|Gibt Überwachungsmeldungen an, die mit der Dialogsicherheit von [!INCLUDE[ssSB](../../includes/sssb-md.md)] verbunden sind.|  
|159|Audit Broker Login|Meldet Überwachungsmeldungen, die mit der Transportsicherheit von [!INCLUDE[ssSB](../../includes/sssb-md.md)] verbunden sind.|  
|160|Broker:Message Undeliverable|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine empfangene Nachricht nicht beibehalten werden kann, die an einen Dienst weitergeleitet werden sollte.|  
|161|Broker:Corrupted Message|Tritt auf, wenn von [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine beschädigte Nachricht empfangen wird.|  
|162|User Error Message|Zeigt Fehlermeldungen an, die für Benutzer im Falle eines Fehlers oder einer Ausnahme angezeigt werden.|  
|163|Broker:Activation|Tritt auf, wenn eine Warteschlangenüberwachung eine gespeicherte Aktivierungsprozedur startet oder eine QUEUE_ACTIVATION-Benachrichtigung sendet oder wenn eine gespeicherte Aktivierungsprozedur, die von einer Warteschlangenüberwachung gestartet wurde, beendet wird.|  
|164|Object:Altered|Tritt auf, wenn ein Datenbankobjekt geändert wird.|  
|165|Performance Statistics|Tritt auf, wenn ein kompilierter Abfrageplan zum ersten Mal zwischengespeichert, erneut kompiliert oder aus dem Plancache gelöscht wird.|  
|166|SQL:StmtRecompile|Tritt auf, wenn eine erneute Kompilierung auf Anweisungsebene durchgeführt wird.|  
|167|Database Mirroring State Change|Tritt auf, wenn sich der Status einer gespiegelten Datenbank ändert.|  
|168|Showplan XML For Query Compile|Tritt auf, wenn eine SQL-Anweisung kompiliert wird. Zeigt die vollständigen Kompilierzeitdaten an. Beachten Sie, dass die **binäre** Spalte für dieses Ereignis den codierten Showplan enthält. Verwenden Sie SQL Server Profiler, um die Ablaufverfolgung zu öffnen und den Showplan anzuzeigen.|  
|169|Showplan All For Query Compile|Tritt auf, wenn eine SQL-Anweisung kompiliert wird. Vollständige, Zeitpunkt der Kompilierung Daten angezeigt Wird verwendet, um Showplanoperatoren anzugeben.|  
|170|Audit Server Scope GDR Event|Gibt an, dass im Serverbereich ein Ereignis zum Erteilen, Aufheben oder Verweigern von Berechtigungen aufgetreten ist, wie z. B. das Erstellen eines Anmeldenamens.|  
|171|Audit Server Object GDR Event|Gibt an, dass ein Ereignis zum Erteilen, Aufheben oder Verweigern für ein Schemaobjekt, wie z. B. eine Tabelle oder Funktion, aufgetreten ist.|  
|172|Audit Database Object GDR Event|Gibt an, dass ein Ereignis zum Erteilen, Aufheben oder Verweigern für Datenbankobjekte, wie z. B. Assemblys und Schemas, aufgetreten ist.|  
|173|Audit Server Operation Event|Tritt auf, wenn Sicherheitsüberwachungsvorgänge verwendet werden, wie z. B. das Ändern von Einstellungen, Ressourcen, des externen Zugriffs oder von Berechtigungen.|  
|175|Audit Server Alter Trace Event|Tritt auf, wenn eine Anweisung die ALTER TRACE-Berechtigung überprüft.|  
|176|Audit Server Object Management Event|Tritt auf, wenn Serverobjekte erstellt, geändert oder gelöscht werden.|  
|177|Audit Server Principal Management Event|Tritt auf, wenn Serverprinzipale erstellt, geändert oder gelöscht werden.|  
|178|Audit Database Operation Event|Tritt auf, wenn Datenbankvorgänge auftreten, wie z. B. CHECKPOINT oder SUBSCRIBE QUERY NOTIFICATIONS.|  
|180|Audit Database Object Access Event|Tritt auf beim Zugriff auf Datenbankobjekte, wie z. B. Schemas.|  
|181|TM: Begin Tran starting|Tritt auf, wenn eine BEGIN TRANSACTION-Anforderung gestartet wird.|  
|182|TM: Begin Tran completed|Tritt auf, wenn eine BEGIN TRANSACTION-Anforderung abgeschlossen wird.|  
|183|TM: Promote Tran starting|Tritt auf, wenn eine PROMOTE TRANSACTION-Anforderung gestartet wird.|  
|184|TM: Promote Tran completed|Tritt auf, wenn eine PROMOTE TRANSACTION-Anforderung abgeschlossen wird.|  
|185|TM: Commit Tran starting|Tritt auf, wenn eine COMMIT TRANSACTION-Anforderung gestartet wird.|  
|186|TM: Commit Tran completed|Tritt auf, wenn eine COMMIT TRANSACTION-Anforderung abgeschlossen wird.|  
|187|TM: Rollback Tran starting|Tritt auf, wenn eine ROLLBACK TRANSACTION-Anforderung gestartet wird.|  
|188|TM: Rollback Tran completed|Tritt auf, wenn eine ROLLBACK TRANSACTION-Anforderung abgeschlossen wird.|  
|189|Lock:Timeout (timeout > 0)|Tritt auf bei einer Zeitüberschreitung für eine Anforderung einer Sperre auf eine Ressource, wie z. B. eine Seite.|  
|190|Progress Report: Online Index Operation|Meldet den Fortschritt einer Onlineindexerstellung, während der Erstellungsprozess ausgeführt wird.|  
|191|TM: Save Tran starting|Tritt auf, wenn eine SAVE TRANSACTION-Anforderung gestartet wird.|  
|192|TM: Save Tran completed|Tritt auf, wenn eine SAVE TRANSACTION-Anforderung abgeschlossen wird.|  
|193|Background Job Error|Tritt auf, wenn ein Hintergrundauftrag fehlerbedingt beendet wurde.|  
|194|OLEDB Provider Information|Tritt auf, wenn eine verteilte Abfrage ausgeführt wird und Informationen sammelt, die sich auf die Anbieterverbindung beziehen.|  
|195|Mount Tape|Tritt auf, wenn eine Anforderung zur Bandeinlegung empfangen wird.|  
|196|Assembly Load|Tritt auf, wenn eine Anforderung zum Laden einer CLR-Assembly auftritt.|  
|197|Reserviert.||  
|198|XQuery Static Type|Tritt auf, wenn ein XQuery-Ausdruck ausgeführt wird. Diese Ereignisklasse stellt den statischen Typ des XQuery-Ausdrucks bereit.|  
|199|QN: Abonnement|Tritt auf, wenn kein Abonnement für die Registrierung einer Abfrage möglich ist. Die **TextData** Spalte enthält Informationen zum Ereignis.|  
|200|QN: parameter table|Informationen zu aktiven Abonnements werden in internen Parametertabellen gespeichert. Diese Ereignisklasse tritt dann auf, wenn eine Parametertabelle angelegt oder gelöscht wird. In der Regel werden diese Tabellen erstellt oder gelöscht, wenn die Datenbank neu gestartet wird. Die **TextData** Spalte enthält Informationen zum Ereignis.|  
|201|template|Eine Abfragevorlage stellt eine Klasse von Abonnementabfragen dar. In der Regel sind Abfragen derselben Klasse mit Ausnahme der Parameterwerte identisch. Diese Ereignisklasse tritt dann auf, wenn eine neue Abfrageanforderung zu einer bereits vorhanden Klasse (Match), einer neue Klasse (Create) oder einer Klasse vom Typ Drop gehört, die Vorlagencleanups für Abfrageklassen ohne aktive Abonnements angibt. Die **TextData** Spalte enthält Informationen zum Ereignis.|  
|202|QN: dynamics|Verfolgt interne Aktivitäten von Abfragebenachrichtigungen nach. Die **TextData** Spalte enthält Informationen zum Ereignis.|  
|212|Bitmapwarnung|Zeigt an, wenn Bitmap-Filter in einer Abfrage deaktiviert wurden.|  
|213|Database Suspect Data Page|Gibt an, wann eine Seite hinzugefügt wird die **Suspect_pages** in Tabelle **Msdb**.|  
|214|CPU threshold exceeded|Zeigt an, dass die Ressourcenkontrolle erkannt hat, dass eine Abfrage den CPU-Grenzwert (REQUEST_MAX_CPU_TIME_SEC) überschritten hat.|  
|215|Zeigt an, dass die Ausführung eines LOGON-Triggers oder einer Klassifizierungsfunktion der Ressourcenkontrolle beginnt.|Zeigt an, dass die Ausführung eines LOGON-Triggers oder einer Klassifizierungsfunktion der Ressourcenkontrolle beginnt.|  
|216|PreConnect:Completed|Gibt an, wenn ein LOGON-Triggers oder der Klassifizierungsfunktion der Ressourcenkontrolle Ausführung abgeschlossen ist.|  
|217|Plan Guide Successful|Zeigt an, dass SQL Server erfolgreich einen Ausführungsplan für eine Abfrage oder einen Batch mit einer Planhinweisliste erzeugt hat.|  
|218|Plan Guide Unsuccessful|Zeigt an, dass SQL Server keinen Ausführungsplan für eine Abfrage oder einen Batch mit einer Planhinweisliste erzeugen konnte. SQL Server hat versucht, einen Ausführungsplan für diese Abfrage oder den Batch zu generieren, ohne die Planhinweisliste anzuwenden. Eine ungültige Planhinweisliste ist möglicherweise die Ursache dieses Problems. Die neue Systemfunktion "sys.fn_validate_plan_guide" kann zur Überprüfung einer Planhinweisliste verwendet werden.|  
|235|Audit Fulltext||  
  
 [  **@columnid=** ] *Column_id*  
 Die ID der Spalte, die für das Ereignis hinzugefügt werden soll. *Column_id* ist **Int**, hat keinen Standardwert.  
  
 In der folgenden Tabelle sind die Spalten aufgeführt, die für ein Ereignis hinzugefügt werden können.  
  
|Spaltennummer|Spaltenname|Description|  
|-------------------|-----------------|-----------------|  
|1|**TextData**|Ein Textwert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wird.|  
|2|**BinaryData**|Binärer Wert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wird.|  
|3|**DatabaseID**|ID der Datenbank, die durch die Verwendung angegebene *Datenbank* -Anweisung oder der Standarddatenbank, wenn keine USE *Datenbank* -Anweisung für eine bestimmte Verbindung ausgegeben wird.<br /><br /> Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion bestimmt werden.|  
|4|**TransactionID**|Die vom System zugewiesene ID der Transaktion.|  
|5|**LineNumber**|Enthält die Nummer der Zeile mit dem Fehler. Für Ereignisse, an denen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen beteiligt sind, wie z. B. **SP:StmtStarting**, enthält der Wert von **LineNumber** die Zeilennummer der Anweisung in der gespeicherten Prozedur oder dem Batch.|  
|6|**NTUserName**|Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzername.|  
|7|**NTDomainName**|Windows-Domäne, zu der der Benutzer gehört.|  
|8|**HostName**|Der Name des Clientcomputers, von dem die Anforderung stammt.|  
|9|**ClientProcessID**|Die ID, die vom Clientcomputer dem Prozess zugewiesen wird, in dem die Clientanwendung ausgeführt wird.|  
|10|**ApplicationName**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|11|**LoginName**|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename des Clients.|  
|12|**SPID**|Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|  
|13|**Dauer**|Die vom Ereignis benötigte Zeitspanne (in Millisekunden). Diese Datenspalte wird nicht durch das Hash Warning-Ereignis aufgefüllt.|  
|14|**StartTime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar).|  
|15|**EndTime**|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen, wie z. B. **SQL:BatchStarting** oder **SP:Starting**, nicht aufgefüllt. Es werden auch nicht ausgefüllt, indem die **Hash Warning** Ereignis.|  
|16|**Reads**|Die Anzahl der logischen Lesevorgänge auf dem Datenträger, die vom Server aufgrund dieses Ereignisses ausgeführt werden. Diese Spalte wird nicht aufgefüllt, indem die **Sperre: freigegeben** Ereignis.|  
|17|**Writes**|Die Anzahl physischer Schreibvorgänge auf dem Datenträger, die vom Server aufgrund des Ereignisses ausgeführt werden.|  
|18|**CPU**|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|19|**Berechtigungen**|Stellt die Bitmap der Berechtigungen dar; wird von Security Auditing verwendet.|  
|20|**Severity**|Schweregrad einer Ausnahme.|  
|21|**EventSubClass**|Der Typ der Ereignisunterklasse. Diese Datenspalte wird nicht für alle Ereignisklassen aufgefüllt.|  
|22|**ObjectID**|Vom System zugewiesene ID des Objekts.|  
|23|**Success**|Erfolg der Berechtigungsverwendung; wird für die Überwachung verwendet.<br /><br /> **1** = Erfolg**0** = Fehler|  
|24|**IndexID**|ID für den Index des Objekts, das von dem Ereignis betroffen ist. Sie können die Index-ID für ein Objekt mithilfe der **indid** -Spalte der **sysindexes** -Systemtabelle ermitteln.|  
|25|**IntegerData**|Wert für eine ganze Zahl, der von der in der Ablaufverfolgung erfassten Ereignisklasse abhängt.|  
|26|**ServerName**|Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], entweder *Servername* oder *Servername\instancename*, verfolgt wird.|  
|27|**EventClass**|Typ der aufgezeichneten Ereignisklasse.|  
|28|**ObjectType**|Der Typ des Objekts, z. B. Tabelle, Funktion oder gespeicherte Prozedur.|  
|29|**NestLevel**|Die Schachtelungsebene, auf der diese gespeicherte Prozedur ausgeführt wird. Finden Sie unter [@@NESTLEVEL &#40; Transact-SQL &#41; ](../../t-sql/functions/nestlevel-transact-sql.md).|  
|30|**Status**|Der Serverstatus im Fall eines Fehlers.|  
|31|**Fehler**|Fehlernummer.|  
|32|**Mode**|Der Sperrmodus der aktivierten Sperre. Diese Spalte wird nicht aufgefüllt, indem die **Sperre: freigegeben** Ereignis.|  
|33|**Handle**|Das Handle des Objekts, auf das im Ereignis verwiesen wird.|  
|34|**ObjectName**|Der Name des Objekts, auf das zugegriffen wird.|  
|35|**DatabaseName**|Name der Datenbank, in die Verwendung angegebene *Datenbank* Anweisung.|  
|36|**FileName**|Der logische Name für den Dateinamen, der geändert wird.|  
|37|**OwnerName**|Der Name des Besitzers des Objekts, auf das verwiesen wird.|  
|38|**RoleName**|Der Name der Datenbankrolle oder der serverweiten Rolle, die Ziel einer Anweisung ist.|  
|39|**TargetUserName**|Der Benutzername des Ziels einer Aktion.|  
|40|**DBUserName**|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankbenutzername des Clients.|  
|41|**LoginSid**|Die Sicherheits-ID (Security Identifier, SID) des angemeldeten Benutzers.|  
|42|**TargetLoginName**|Der Anmeldename des Ziels einer Aktion.|  
|43|**TargetLoginSid**|Die SID des Anmeldenamens, der Ziel einer Aktion ist.|  
|44|**ColumnPermissions**|Berechtigungsstatus auf Spaltenebene; wird von Security Auditing verwendet.|  
|45|**LinkedServerName**|Name des Verbindungsservers|  
|46|**ProviderName**|Name des OLE DB-Anbieters.|  
|47|**MethodName**|Der Name der OLE DB-Methode.|  
|48|**RowCounts**|Die Anzahl von Zeilen im Batch.|  
|49|**RequestID**|Die ID der Anforderung, die die Anweisung enthält.|  
|50|**XactSequence**|Ein Token zur Beschreibung der aktuellen Transaktion.|  
|51|**EventSequence**|Die Sequenznummer für dieses Ereignis.|  
|52|**BigintData1**|**"bigint"** Wert, der der in der Ablaufverfolgung erfassten Ereignisklasse abhängt.|  
|53|**BigintData2**|**"bigint"** Wert, der der in der Ablaufverfolgung erfassten Ereignisklasse abhängt.|  
|54|**GUID**|Der GUID-Wert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wurde.|  
|55|**IntegerData2**|Der ganzzahlige Wert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wurde.|  
|56|**ObjectID2**|Die ID des verbundenen Objekts oder der verbundenen Entität (falls verfügbar).|  
|57|**Typ**|Der ganzzahlige Wert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wurde.|  
|58|**OwnerID**|Der Typ des Objekts, das die Sperre besitzt. Nur für Sperrereignisse.|  
|59|**ParentName**|Der Name des Schemas, in dem sich das Objekt befindet.|  
|60|**IsSystem**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist.<br /><br /> **1** = System<br /><br /> **0** = Benutzer.|  
|61|**Offset**|Der Startoffset der Anweisung in der gespeicherten Prozedur oder im Batch.|  
|62|**SourceDatabaseID**|Die ID der Datenbank, in der sich die Quelle des Objekts befindet.|  
|63|**SqlHandle**|64-Bit-Hash, der auf dem Text einer Ad-hoc-Abfrage oder der Datenbank- und Objekt-ID eines SQL-Objekts basiert. Dieser Wert kann an **sys.dm_exec_sql_text()** übergeben werden, um den dazugehörigen SQL-Text abzurufen.|  
|64|**SessionLoginName**|Anmeldename des Benutzers, der die Sitzung geöffnet hat. Wenn Sie beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Login1 **verwenden, um eine Verbindung mit** herzustellen, und eine Anweisung als **Login2**ausführen, zeigt **SessionLoginName** den Wert **Login1**an und **LoginName** den Wert **Login2**. In dieser Datenspalte werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - und Windows-Anmeldenamen angezeigt.|  
  
 **[ @on=]** *auf*  
 Gibt an, ob das Ereignis auf ON (1) oder OFF (0) festgelegt werden soll. *auf* ist **Bit**, hat keinen Standardwert.  
  
 Wenn *auf* festgelegt ist, um **1**, und *Column_id* NULL ist, und klicken Sie dann das Ereignis auf ON festgelegt ist und alle Spalten werden gelöscht. Wenn *Column_id* nicht null ist, und klicken Sie dann die Spalte für dieses Ereignis auf ON festgelegt ist.  
  
 Wenn *auf* festgelegt ist, um **0**, und *Column_id* NULL ist, wird das Ereignis deaktiviert OFF und alle Spalten werden gelöscht. Wenn *Column_id* nicht null ist, und klicken Sie dann die Spalte aktiviert ist OFF.  
  
 Die folgende Tabelle zeigt die Interaktion zwischen  **@on**  und  **@columnid** .  
  
|@on|@columnid|Ergebnis|  
|---------|---------------|------------|  
|ON (**1**)|NULL|Das Ereignis ist aktiviert (ON).<br /><br /> Alle Spalten werden gelöscht.|  
||NOT NULL|Die Spalte ist für das angegebene Ereignis aktiviert (ON).|  
|OFF (**0**)|NULL|Das Ereignis ist deaktiviert (OFF).<br /><br /> Alle Spalten werden gelöscht.|  
||NOT NULL|Die Spalte ist für das angegebene Ereignis deaktiviert (OFF).|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In der folgenden Tabelle werden die Codewerte beschrieben, die die Benutzer nach Abschluss der gespeicherten Prozedur möglicherweise erhalten.  
  
|Rückgabecode|Beschreibung|  
|-----------------|-----------------|  
|0|Kein Fehler.|  
|1|Unbekannter Fehler.|  
|2|Die Ablaufverfolgung wird derzeit ausgeführt. Wenn die Ablaufverfolgung jetzt geändert wird, hat dies einen Fehler zur Folge.|  
|3|Das angegebene Ereignis ist ungültig. Das Ereignis ist möglicherweise nicht vorhanden oder nicht für die gespeicherte Prozedur geeignet.|  
|4|Die angegebene Spalte ist ungültig.|  
|9|Das angegebene Ablaufverfolgungshandle ist ungültig.|  
|11|Die angegebene Spalte wird intern verwendet und kann nicht entfernt werden.|  
|13|Nicht genügend Arbeitsspeicher. Wird zurückgegeben, wenn nicht genügend Arbeitsspeicher zum Ausführen der angegebenen Aktion verfügbar ist.|  
|16|Die Funktion ist für diese Ablaufverfolgung ungültig.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_trace_setevent** führt viele der Aktionen, die von erweiterten gespeicherten Prozeduren, die in früheren Versionen von zuvor ausgeführten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwendung **Sp_trace_setevent** anstatt die folgende:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_eventclassrequired**  
  
-   **xp_trace_seteventclassrequired**  
  
 Benutzer müssen ausführen **Sp_trace_setevent** für jede Spalte, die für jedes Ereignis hinzugefügt. Während jeder Ausführung Wenn  **@on**  festgelegt ist, um **1**, **Sp_trace_setevent** fügt das angegebene Ereignis in die Liste der Ereignisliste der Ablaufverfolgung. Wenn  **@on**  festgelegt ist, um **0**, **Sp_trace_setevent** entfernt das angegebene Ereignis aus der Liste.  
  
 Parameter aller gespeicherten Prozeduren der SQL-Ablaufverfolgung (**sp_trace_xx**) haben eine strikte Typbindung. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
 Ein Beispiel zum Verwenden gespeicherter Prozeduren der Ablaufverfolgung finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER TRACE-Berechtigung verfügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. fn_trace_geteventinfo &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 ["sp_trace_generateevent" &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  
