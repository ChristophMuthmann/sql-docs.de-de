---
title: Sys. dm_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_requests_TSQL
- sys.dm_exec_requests
- dm_exec_requests_TSQL
- dm_exec_requests
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_requests dynamic management view
ms.assetid: 4161dc57-f3e7-4492-8972-8cfb77b29643
caps.latest.revision: 67
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 51f71a3274031ad3a9a795e94fa0c15968fc2bfa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecrequests-transact-sql"></a>sys.dm_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen über jede einzelne Anforderung, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, zurück.  
  
> [!NOTE]  
>  Für die Ausführung von Code außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (z. B. erweiterte gespeicherte Prozeduren und verteilte Abfragen) muss ein Thread außerhalb der Steuerung des nicht präemptiven Zeitplanungsmoduls ausgeführt werden. Dazu wechselt ein Arbeitsthread in den präemptiven Modus. Zeitwerte, die von dieser dynamischen Verwaltungssicht zurückgegeben werden, schließen nicht die im präemptiven Modus verbrachte Zeit ein.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|ID der Sitzung, auf die sich diese Anforderung bezieht. Lässt keine NULL-Werte zu.|  
|request_id|**int**|ID der Anforderung. Ist im Kontext der Sitzung eindeutig. Lässt keine NULL-Werte zu.|  
|start_time|**datetime**|Der Zeitstempel, der angibt, wann die Anforderung eingetroffen ist. Lässt keine NULL-Werte zu.|  
|status|**nvarchar(30)**|Status der Anforderung. Die folgenden Werte sind möglich:<br /><br /> Hintergrund<br />Wird ausgeführt<br />Ausführbar<br />Ruhezustand<br />Angehalten<br /><br /> Lässt keine NULL-Werte zu.|  
|Befehl|**nvarchar(32)**|Identifiziert den aktuellen Typ des Befehls, der gerade verarbeitet wird. Als allgemeine Befehlstypen sind die folgenden möglich:<br /><br /> SELECT<br />INSERT<br />UPDATE<br />DELETE<br />BACKUP LOG<br />BACKUP DATABASE<br />DBCC<br />FOR<br /><br /> Der Text der Anforderung kann mithilfe von sys.dm_exec_sql_text und dem entsprechenden sql_handle-Wert für die Anforderung abgerufen werden. Interne Systemprozesse legen den Befehl je nach Typ des ausgeführten Tasks fest. Mögliche Tasks sind z. B. die folgenden:<br /><br /> LOCK MONITOR<br />CHECKPOINTLAZY<br />WRITER<br /><br /> Lässt keine NULL-Werte zu.|  
|sql_handle|**varbinary(64)**|Hashzuordnung des SQL-Texts der Anforderung. Lässt NULL-Werte zu.|  
|statement_start_offset|**int**|Anzahl von Zeichen im derzeit ausgeführten Batch oder in der derzeit ausgeführten gespeicherten Prozedur, an der die derzeit ausgeführte Anweisung beginnt. Kann zusammen mit sql_handle, statement_end_offset und der dynamischen Verwaltungsfunktion sys.dm_exec_sql_text zum Abrufen der zurzeit ausgeführten Anweisung für die Anforderung verwendet werden. Lässt NULL-Werte zu.|  
|statement_end_offset|**int**|Anzahl von Zeichen im derzeit ausgeführten Batch oder in der derzeit ausgeführten gespeicherten Prozedur, an der die derzeit ausgeführte Anweisung endet. Kann zusammen mit sql_handle, statement_end_offset und der dynamischen Verwaltungsfunktion sys.dm_exec_sql_text zum Abrufen der zurzeit ausgeführten Anweisung für die Anforderung verwendet werden. Lässt NULL-Werte zu.|  
|plan_handle|**varbinary(64)**|Hashzuordnung des Plans für die SQL-Ausführung. Lässt NULL-Werte zu.|  
|database_id|**smallint**|ID der Datenbank, für die die Anforderung ausgeführt wird. Lässt keine NULL-Werte zu.|  
|user_id|**int**|ID des Benutzers, der die Anforderung gesendet hat. Lässt keine NULL-Werte zu.|  
|connection_id|**uniqueidentifier**|ID der Verbindung, über die die Anforderung eingetroffen ist. Lässt NULL-Werte zu.|  
|blocking_session_id|**smallint**|ID der Sitzung, die die Anforderung blockiert. Wenn diese Spalte den Wert NULL aufweist, wird die Anforderung nicht blockiert, oder die Sitzungsinformationen der blockierenden Sitzung sind nicht verfügbar (bzw. können nicht identifiziert werden).<br /><br /> -2 = Der Besitzer der blockierenden Ressource ist eine verwaiste verteilte Transaktion.<br /><br /> -3 = Der Besitzer der blockierenden Ressource ist eine verzögerte Wiederherstellungstransaktion.<br /><br /> -4 = Die Sitzungs-ID des Besitzers des blockierenden Latches konnte zu diesem Zeitpunkt aufgrund von internen Latchstatusübergängen nicht bestimmt werden.|  
|wait_type|**nvarchar(60)**|Wenn die Anforderung zurzeit blockiert wird, gibt diese Spalte den Wartetyp zurück. Lässt NULL-Werte zu.<br /><br /> Informationen zu Wartetypen finden Sie unter [dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|wait_time|**int**|Wenn die Anforderung zurzeit blockiert wird, gibt diese Spalte die Dauer des aktuellen Wartevorgangs in Millisekunden an. Lässt keine NULL-Werte zu.|  
|last_wait_type|**nvarchar(60)**|Wenn diese Anforderung zuvor bereits blockiert war, gibt diese Spalte den Typ des letzten Wartevorgangs zurück. Lässt keine NULL-Werte zu.|  
|wait_resource|**nvarchar(256)**|Wenn die Anforderung zurzeit blockiert wird, gibt diese Spalte die Ressource zurück, auf die die Anforderung zurzeit wartet. Lässt keine NULL-Werte zu.|  
|open_transaction_count|**int**|Anzahl der für die Anforderung offenen Transaktionen. Lässt keine NULL-Werte zu.|  
|open_resultset_count|**int**|Anzahl der für die Anforderung offenen Resultsets. Lässt keine NULL-Werte zu.|  
|transaction_id|**bigint**|ID der Transaktion, in der diese Anforderung ausgeführt wird. Lässt keine NULL-Werte zu.|  
|context_info|**varbinary(128)**|CONTEXT_INFO-Wert der Sitzung. Lässt NULL-Werte zu.|  
|percent_complete|**real**|Prozentsatz der für die folgenden Befehle durchgeführten Arbeit:<br /><br /> ALTER INDEX REORGANIZE<br />AUTO_SHRINK-Option mit ALTER DATABASE<br />BACKUP DATABASE<br />DBCC CHECKDB<br />DBCC CHECKFILEGROUP<br />DBCC CHECKTABLE<br />DBCC INDEXDEFRAG<br />DBCC SHRINKDATABASE<br />DBCC SHRINKFILE<br />RECOVERY<br />RESTORE DATABASE<br />ROLLBACK<br />TDE ENCRYPTION<br /><br /> Lässt keine NULL-Werte zu.|  
|estimated_completion_time|**bigint**|Nur intern. Lässt keine NULL-Werte zu.|  
|cpu_time|**int**|Von der Anforderung beanspruchte CPU-Zeit (in Millisekunden). Lässt keine NULL-Werte zu.|  
|total_elapsed_time|**int**|Gesamtzeit seit dem Eintreffen der Anforderung (in Millisekunden). Lässt keine NULL-Werte zu.|  
|scheduler_id|**int**|ID des Zeitplanungsmoduls, das diese Anforderung plant. Lässt keine NULL-Werte zu.|  
|task_address|**varbinary(8)**|Speicheradresse, die dem Task für diese Anforderung zugeordnet ist. Lässt NULL-Werte zu.|  
|reads|**bigint**|Anzahl der von dieser Anforderung ausgeführten Lesevorgänge. Lässt keine NULL-Werte zu.|  
|writes|**bigint**|Anzahl der von dieser Anforderung ausgeführten Schreibvorgänge. Lässt keine NULL-Werte zu.|  
|logical_reads|**bigint**|Anzahl der von dieser Anforderung ausgeführten logischen Lesevorgänge. Lässt keine NULL-Werte zu.|  
|text_size|**int**|TEXTSIZE-Einstellung für diese Anforderung. Lässt keine NULL-Werte zu.|  
|Sprache|**nvarchar(128)**|Spracheinstellung für die Anforderung. Lässt NULL-Werte zu.|  
|date_format|**nvarchar(3)**|DATEFORMAT-Einstellung für die Anforderung. Lässt NULL-Werte zu.|  
|date_first|**smallint**|DATEFIRST-Einstellung für die Anforderung. Lässt keine NULL-Werte zu.|  
|quoted_identifier|**bit**|1 = QUOTED_IDENTIFIER ist ON für die Anforderung. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|arithabort|**bit**|1 = ARITHABORT ist für die Anforderung auf ON festgelegt. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|ansi_null_dflt_on|**bit**|1 = ANSI_NULL_DFLT_ON ist für die Anforderung auf ON festgelegt. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|ansi_defaults|**bit**|1 = ANSI_DEFAULTS ist für die Anforderung auf ON festgelegt. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|ansi_warnings|**bit**|1 = ANSI_WARNINGS ist für die Anforderung auf ON festgelegt. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|ansi_padding|**bit**|1 = ANSI_PADDING ist für die Anforderung auf ON festgelegt.<br /><br /> Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|ansi_nulls|**bit**|1 = ANSI_NULLS ist für die Anforderung auf ON festgelegt. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|concat_null_yields_null|**bit**|1 = CONCAT_NULL_YIELDS_NULL ist für die Anforderung auf ON festgelegt. Andernfalls ist der Wert 0.<br /><br /> Lässt keine NULL-Werte zu.|  
|transaction_isolation_level|**smallint**|Isolationsstufe, mit der die Transaktion für diese Anforderung erstellt wird. Lässt keine NULL-Werte zu.<br /><br /> 0 = Unspecified<br /><br /> 1 = ReadUncomitted<br /><br /> 2 = ReadCommitted<br /><br /> 3 = Repeatable<br /><br /> 4 = Serializable<br /><br /> 5 = Momentaufnahme|  
|lock_timeout|**int**|Sperrtimeout für diese Anforderung (in Millisekunden). Lässt keine NULL-Werte zu.|  
|deadlock_priority|**int**|DEADLOCK_PRIORITY-Einstellung für die Anforderung. Lässt keine NULL-Werte zu.|  
|row_count|**bigint**|Anzahl von Zeilen, die von dieser Anforderung an den Client zurückgegeben wurden. Lässt keine NULL-Werte zu.|  
|prev_error|**int**|Letzter Fehler, der während der Ausführung der Anforderung aufgetreten ist. Lässt keine NULL-Werte zu.|  
|nest_level|**int**|Aktuelle Schachtelungsebene von Code, der für die Anforderung ausgeführt wird. Lässt keine NULL-Werte zu.|  
|granted_query_memory|**int**|Anzahl von Seiten, die der Ausführung einer Abfrage in der Anforderung zugeordnet sind. Lässt keine NULL-Werte zu.|  
|executing_managed_code|**bit**|Gibt an, ob eine bestimmte Anforderung zurzeit CLR-Objekte (Common Language Runtime) ausführt, z. B. Routinen, Typen und Trigger. Die Festlegung gilt für die gesamte Zeit, die sich ein CLR-Objekt im Stapel befindet, selbst wenn [!INCLUDE[tsql](../../includes/tsql-md.md)] aus CLR heraus ausgeführt wird. Lässt keine NULL-Werte zu.|  
|group_id|**int**|ID der Arbeitsauslastungsgruppe, zu der diese Abfrage gehört. Lässt keine NULL-Werte zu.|  
|query_hash|**binary(8)**|Binärer Hashwert, der in der Abfrage berechnet wird und zum Identifizieren von Abfragen mit ähnlicher Logik verwendet wird. Sie können den Abfragehash verwenden, um die aggregierte Ressourcennutzung für Abfragen zu ermitteln, die sich nur durch Literalwerte unterscheiden.|  
|query_plan_hash|**binary(8)**|Binärer Hashwert, der im Abfrageausführungsplan wird und zum Identifizieren ähnlicher Abfrageausführungspläne verwendet wird. Sie können diesen Abfrageplan-Hashwert verwenden, um die kumulierten Kosten für Abfragen mit ähnlichen Ausführungsplänen zu suchen.|  
|statement_sql_handle|**varbinary(64)**|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> SQL-Handle die einzelne Abfrage. |  
|statement_context_id|**bigint**|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die optionale Fremdschlüssel sys.query_context_settings. |  
|dop |**int** |**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Der Grad der Parallelität für die Abfrage. |  
|parallel_worker_count |**int** |**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl der reservierten parallelen Arbeitsthreads ist dies eine parallele Abfrage.  |  
|external_script_request_id |**uniqueidentifier** |**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die externen Skript-Anforderungs-ID in der aktuellen Anforderung verknüpft sind. |  
|is_resumable |**bit** |**Gilt für**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, ob die Anforderung einer fortsetzbaren Indexvorgang ausgeführt wurde. |  
  
## <a name="permissions"></a>Berechtigungen  
 Wenn der Benutzer hat `VIEW SERVER STATE` Berechtigung auf dem Server, sieht der Benutzer alle zurzeit ausgeführten Sitzungen für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist, andernfalls der Benutzer sieht nur die aktuelle Sitzung. `VIEW SERVER STATE` kann nicht gewährt werden, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] damit `sys.dm_exec_requests` ist immer auf die aktuelle Verbindung beschränkt. 
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-finding-the-query-text-for-a-running-batch"></a>A. Suchen des Abfragetexts für einen ausgeführten Batch  
 Im folgenden Beispiel werden `sys.dm_exec_requests` abgefragt, um die entsprechende Abfrage zu suchen und den `sql_handle`-Wert aus der Ausgabe zu kopieren.  
  
```  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Verwenden Sie dann zum Abrufen des Anweisungstexts den kopierten `sql_handle`-Wert mit der Systemfunktion `sys.dm_exec_sql_text(sql_handle)`.  
  
```  
SELECT * FROM sys.dm_exec_sql_text(< copied sql_handle >);  
GO  
```  
  
### <a name="b-finding-all-locks-that-a-running-batch-is-holding"></a>B. Suchen aller Sperren, die ein ausgeführter Batch enthält  
 Die folgende Beispielabfrage **Sys. dm_exec_requests** finden Sie die interessanten Batch und kopieren Sie die `transaction_id` aus der Ausgabe.  
  
```  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Verwenden Sie dann zum Suchen von Sperrinformationen den kopierten `transaction_id` mit der Systemfunktion **Sys. dm_tran_locks**.  
  
```  
SELECT * FROM sys.dm_tran_locks   
WHERE request_owner_type = N'TRANSACTION'   
    AND request_owner_id = < copied transaction_id >;  
GO  
```  
  
### <a name="c-finding-all-currently-blocked-requests"></a>C. Suchen aller zurzeit blockierten Anforderungen  
 Die folgende Beispielabfrage **Sys. dm_exec_requests** finden Sie Informationen zu blockierten Anforderungen.  
  
```  
SELECT session_id ,status ,blocking_session_id  
    ,wait_type ,wait_time ,wait_resource   
    ,transaction_id   
FROM sys.dm_exec_requests   
WHERE status = N'suspended';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
