---
title: KILL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs:
- TSQL
helpviewer_keywords:
- WITH STATUSONLY option
- terminating distributed transactions
- distributed transactions [SQL Server], terminating
- in-doubt transactions
- IDs [SQL Server], user processes
- ending distributed transactions [SQL Server]
- stopping distributed transactions
- session IDs [SQL Server]
- system process termination [SQL Server]
- stopping processes
- ending processes [SQL Server]
- UOW [SQL Server]
- orphaned transactions [SQL Server]
- unit of work [SQL Server]
- process termination [SQL Server]
- KILL statement
- terminating process
ms.assetid: 071cf260-c794-4b45-adc0-0e64097938c0
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6460d8ae1b48e99305b6361a29b47ba06e9213f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Beendet einen Benutzerprozess basierend auf der Sitzungs-ID oder Arbeitseinheit (Unit of Work, UOW). Falls für die angegebene Sitzungs-ID oder UOW viele Vorgänge rückgängig gemacht werden müssen, kann die KILL-Anweisung einige Zeit in Anspruch nehmen, besonders wenn dabei ein Rollback für eine lange Transaktion ausgeführt wird.  
  
 KILL kann verwendet werden, um eine normale Verbindung zu beenden, wodurch die der angegebenen Sitzungs-ID zugeordneten Transaktionen intern beendet werden. Die Anweisung kann auch verwendet werden, um verwaiste und unsichere verteilte Transaktionen zu beenden, wenn [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) verwendet wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
KILL { session ID | UOW } [ WITH STATUSONLY ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
KILL 'session_id'  
[;]   
```  
  
## <a name="arguments"></a>Argumente  
 *Sitzungs-ID*  
 Die Sitzungs-ID des Prozesses, der beendet werden soll. Die *Sitzungs-ID* ist eine eindeutige ganze Zahl (**int**), die jeder Benutzerverbindung beim Herstellen der Verbindung zugewiesen wird. Der Sitzungs-ID-Wert ist für die Dauer der Verbindung an die Verbindung gebunden. Beim Beenden der Verbindung wird der ganzzahlige Wert freigegeben und kann einer neuen Verbindung zugewiesen werden.  
Bei der Suche nach der `session_id`, die Sie beenden möchten, kann folgende Abfrage hilfreich sein:  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Identifiziert die Arbeitseinheits-ID (UOW) verteilter Transaktionen. *UOW* ist eine GUID, die aus der Spalte „request_owner_guid“ der dynamischen Verwaltungssicht „sys.dm_tran_locks“ abgerufen werden kann. *UOW* kann auch aus dem Fehlerprotokoll oder über den MS DTC-Monitor ermittelt werden. Weitere Informationen zum Überwachen von verteilten Transaktionen finden Sie in der MS DTC-Dokumentation.  
  
 Verwenden Sie KILL *UOW* zum Beenden verwaister verteilter Transaktionen. Diese Transaktionen sind keiner echten Sitzungs-ID, sondern künstlich der Sitzungs-ID = '-2' zugeordnet. Diese Sitzungs-ID ermöglicht das Identifizieren verwaister Transaktionen, indem die Sitzungs-ID-Spalte in den dynamischen Verwaltungssichten sys.dm_tran_locks, sys.dm_exec_sessions oder sys.dm_exec_requests abgefragt wird.  
  
 WITH STATUSONLY  
 Generiert einen Fortschrittsbericht für eine angegebene *Sitzungs-ID* oder *UOW*, für den aufgrund einer früheren KILL-Anweisung ein Rollback ausgeführt wird. Durch KILL WITH STATUSONLY wird der von der *Sitzungs-ID* oder *UOW* angegebene Prozess weder beendet noch wird ein Rollback ausgeführt. Es wird lediglich der aktuelle Fortschritt des Rollbacks angezeigt.  
  
## <a name="remarks"></a>Remarks  
 KILL wird üblicherweise zum Beenden von Prozessen verwendet, die andere wichtige Prozesse mit Sperren blockieren, oder von Prozessen, die Abfragen ausführen, die dringend benötigte Systemressourcen belegen. Systemprozesse und Prozesse, die eine erweiterte gespeicherte Prozedur ausführen, können nicht beendet werden.  
  
 Verwenden Sie KILL sorgfältig, besonders wenn kritische Prozesse ausgeführt werden. Ihren eigenen Prozess können Sie nicht beenden. Auch die folgenden Prozesse sollten Sie nicht beenden:  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
Mit @@SPID kann der Sitzungs-ID-Wert der aktuellen Sitzung angezeigt werden.  
  
 Sie können die session_id-Spalte der dynamischen Verwaltungssichten sys.dm_tran_locks, sys.dm_exec_sessions und sys.dm_exec_requests abfragen, um einen Bericht über die aktiven Sitzungs-ID-Werte zu erhalten. Sie können auch die SPID-Spalte anzeigen, die von der gespeicherten Systemprozedur sp_who zurückgegeben wird. Wenn für einen bestimmten SPID-Wert ein Rollback ausgeführt wird, enthält die cmd-Spalte im sp_who-Resultset für diesen SPID-Wert den Eintrag KILLED/ROLLBACK.  
  
 Wenn eine bestimmte Verbindung eine Datenbankressource sperrt und den Fortschritt einer anderen Transaktion blockiert, wird die Sitzungs-ID der blockierenden Verbindung in der `blocking_session_id`-Spalte von `sys.dm_exec_requests` oder der von `blk` zurückgegebenen `sp_who`-Spalte angezeigt.  
  
 Der KILL-Befehl kann zum Auflösen von unsicheren verteilten Transaktionen verwendet werden. Bei diesen Transaktionen handelt es sich um nicht aufgelöste verteilte Transaktionen, die aufgrund unplanmäßiger Neustarts des Datenbankservers oder von MS DTC (Microsoft Distributed Transaction Coordinator) auftreten. Weitere Informationen über unsichere Transaktionen finden Sie im Abschnitt „Zweiphasencommit“ unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>Verwenden von WITH STATUSONLY  
 KILL WITH STATUSONLY generiert nur dann einen Bericht, wenn aufgrund einer früheren Anweisung KILL *session ID*|*UOW* derzeit ein Rollback für die Sitzungs-ID oder UOW ausgeführt wird. Der Fortschrittsbericht enthält den Prozentsatz, zu dem der Rollbackvorgang abgeschlossen ist, und die geschätzte Dauer der verbleibenden Zeit (in Sekunden) in folgender Form:  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 Ist das Rollback der Sitzungs-ID oder UOW zum Zeitpunkt der Ausführung der Anweisung KILL *session ID*|*UOW* WITH STATUSONLY bereits abgeschlossen oder wird kein Rollback für die Sitzungs-ID oder UOW ausgeführt, gibt KILL *session ID*|*UOW* WITH STATUSONLY folgende Fehlermeldung zurück:  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 Der gleiche Statusbericht wird durch Wiederholen der gleichen Anweisung KILL *session ID*|*UOW* ohne die WITH STATUSONLY-Option erstellt. Dies wird allerdings nicht empfohlen. Durch das Wiederholen einer KILL *session ID*-Anweisung wird möglicherweise ein neuer Prozess beendet, falls das Rollback bereits abgeschlossen war und die Sitzungs-ID vor der Ausführung der neuen KILL-Anweisung einem neuen Task zugewiesen worden ist. Mit der Angabe von WITH STATUSONLY wird dies verhindert.  
  
## <a name="permissions"></a>Berechtigungen  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** Erfordert die Berechtigung ALTER ANY CONNECTION. ALTER ANY CONNECTION ist mit der Mitgliedschaft in den festen Serverrollen sysadmin und processadmin verbunden.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:** Erfordert die Berechtigung KILL DATABASE CONNECTION. Das Prinzipalkonto auf Serverebene verfügt über die Berechtigung KILL DATABASE CONNECTION.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-kill-to-terminate-a-session"></a>A. Verwenden von KILL zum Beenden einer Sitzung  
 Im folgenden Beispiel wird gezeigt, wie die Sitzungs-ID `53` beendet wird.  
  
```sql  
KILL 53;  
GO  
```  
  
### <a name="b-using-kill-session-id-with-statusonly-to-obtain-a-progress-report"></a>B. Verwenden von KILL Sitzungs-ID WITH STATUSONLY zum Anzeigen eines Fortschrittsberichts  
 Im folgenden Beispiel wird ein Statusbericht für den Rollbackvorgang der angegebenen Sitzungs-ID generiert.  
  
```sql  
KILL 54;  
KILL 54 WITH STATUSONLY;  
GO  
  
--This is the progress report.  
spid 54: Transaction rollback in progress. Estimated rollback completion: 80% Estimated time left: 10 seconds.  
```  
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. Verwenden von KILL zum Beenden einer verwaisten verteilten Transaktion  
 Im folgenden Beispiel wird gezeigt, wie eine verwaiste verteilte Transaktion (session ID = -2) mit einem *UOW* von `D5499C66-E398-45CA-BF7E-DC9C194B48CF` beendet wird.  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
