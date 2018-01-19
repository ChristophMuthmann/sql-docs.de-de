---
title: Sys. dm_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_sessions_TSQL
- sys.dm_exec_sessions
- dm_exec_sessions
- sys.dm_exec_sessions_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_sessions dynamic management view
ms.assetid: 2b7e8e0c-eea0-431e-819f-8ccd12ec8cfa
caps.latest.revision: "60"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5e0cd35b044d4a5016442ddae4384aea094cc655
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sysdmexecsessions-transact-sql"></a>sys.dm_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile pro authentifizierter Sitzung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück. sys.dm_exec_sessions ist eine Sicht des Serverbereichs mit Informationen zu allen aktiven Benutzerverbindungen und internen Tasks. Zu diesen Informationen zählen u. a. die Clientversion, der Name des Clientprogramms, die Clientanmeldezeit, der angemeldete Benutzer und die aktuelle Sitzungseinstellung. Mit sys.dm_exec_sessions zeigen Sie zuerst die aktuelle Systemauslastung an und identifizieren eine interessante Sitzung, und informieren Sie sich dann in dynamischen Verwaltungssichten oder dynamischen Verwaltungsfunktionen weiter über diese Sitzung.  
  
 Die dynamischen Verwaltungssichten Sys. dm_exec_connections, Sys. dm_exec_sessions und Sys. dm_exec_requests Zuordnen der [sys.sysprocesses](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) -Systemtabelle.  
  
> **Hinweis:** von Aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_exec_sessions**.  
  
|Spaltenname|Datentyp|Beschreibung und versionsspezifische Informationen|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifiziert die einer aktiven primären Verbindung zugeordnete Sitzung. Lässt keine NULL-Werte zu.|  
|login_time|**datetime**|Uhrzeit, zu der die Sitzung eingerichtet wurde. Lässt keine NULL-Werte zu.|  
|host_name|**nvarchar(128)**|Name der für eine Sitzung spezifischen Clientarbeitsstation. Der Wert ist für interne Sitzungen NULL. Lässt NULL-Werte zu.<br /><br /> **Sicherheitshinweis:** die Clientanwendung stellt den Namen der Arbeitsstation und kann fehlerhafte Daten angeben. Verwenden Sie HOST_NAME nicht als Sicherheitsfunktion.|  
|program_name|**nvarchar(128)**|Name des Clientprogramms, mit dem die Sitzung initiiert wurde. Der Wert ist für interne Sitzungen NULL. Lässt NULL-Werte zu.|  
|host_process_id|**int**|Prozess-ID des Clientprogramms, mit dem die Sitzung initiiert wurde. Der Wert ist für interne Sitzungen NULL. Lässt NULL-Werte zu.|  
|client_version|**int**|Die vom Client für die Verbindung mit dem Server verwendete TDS-Protokollversion der Schnittstelle. Der Wert ist für interne Sitzungen NULL. Lässt NULL-Werte zu.|  
|client_interface_name|**nvarchar(32)**|Name der Bibliothek/Treiber, die vom Client zur Kommunikation mit dem Server verwendet wird. Der Wert ist für interne Sitzungen NULL. Lässt NULL-Werte zu.|  
|security_id|**varbinary(85)**|Microsoft Windows-Sicherheits-ID, die der Anmeldung zugeordnet ist. Lässt keine NULL-Werte zu.|  
|login_name|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename, unter dem die Sitzung gegenwärtig ausgeführt wird. Den ursprünglichen Anmeldenamen, mit dem die Sitzung erstellt wurde, finden Sie unter original_login_name. Kann eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldename oder eine Windows authentifizierter Benutzername Domäne authentifiziert. Lässt keine NULL-Werte zu.|  
|nt_domain|**nvarchar(128)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Windows-Domäne für den Client, wenn für die Sitzung die Windows-Authentifizierung oder eine vertrauenswürdige Verbindung verwendet wird. Dieser Wert ist für interne Sitzungen und andere Benutzer als Domänenbenutzer NULL. Lässt NULL-Werte zu.|  
|nt_user_name|**nvarchar(128)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Der Windows-Benutzername für den Client, wenn für die Sitzung die Windows-Authentifizierung oder eine vertrauenswürdige Verbindung verwendet wird. Dieser Wert ist für interne Sitzungen und andere Benutzer als Domänenbenutzer NULL. Lässt NULL-Werte zu.|  
|status|**nvarchar(30)**|Status der Sitzung. Mögliche Werte:<br /><br /> **Ausführen** -derzeit eine oder mehrere Anforderungen ausführen<br /><br /> **Sleeping** -derzeit keine Anforderungen ausgeführt<br /><br /> **Ruhende** – Sitzung wurde aufgrund des Verbindungspoolings zurückgesetzt und befindet sich nun im Status vor einer Anmeldung.<br /><br /> **Preconnect** -Sitzung ist in der Klassifizierungsfunktion der Ressourcenkontrolle.<br /><br /> Lässt keine NULL-Werte zu.|  
|context_info|**varbinary(128)**|CONTEXT_INFO-Wert für die Sitzung. Die Kontextinformationen vom Benutzer festgelegt ist, mithilfe der [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) Anweisung. Lässt NULL-Werte zu.|  
|cpu_time|**int**|Die von der Sitzung verwendete CPU-Zeit in Millisekunden. Lässt keine NULL-Werte zu.|  
|memory_usage|**int**|Anzahl der von der Sitzung verwendeten 8 KB-Speicherseiten. Lässt keine NULL-Werte zu.|  
|total_scheduled_time|**int**|Gesamtzeit in Millisekunden, die für die Ausführung der Sitzung (sowie der darin enthaltenen Anforderungen) eingeplant wurde. Lässt keine NULL-Werte zu.|  
|total_elapsed_time|**int**|Zeit in Millisekunden seit dem Einrichten der Sitzung. Lässt keine NULL-Werte zu.|  
|endpoint_id|**int**|ID des Endpunktes, der der Sitzung zugeordnet ist. Lässt keine NULL-Werte zu.|  
|last_request_start_time|**datetime**|Uhrzeit, zu der die letzte Anforderung in der Sitzung gestartet wurde. Dies schließt die derzeit ausgeführte Anforderung ein. Lässt keine NULL-Werte zu.|  
|last_request_end_time|**datetime**|Uhrzeit, zu der eine Anforderung in der Sitzung zuletzt abgeschlossen wurde. Lässt NULL-Werte zu.|  
|reads|**bigint**|Anzahl von Lesevorgängen von Anforderungen in dieser Sitzung oder während dieser Sitzung. Lässt keine NULL-Werte zu.|  
|writes|**bigint**|Anzahl der Schreibvorgänge von Anforderungen in dieser Sitzung oder während dieser Sitzung. Lässt keine NULL-Werte zu.|  
|logical_reads|**bigint**|Anzahl von logischen Lesevorgängen in der Sitzung. Lässt keine NULL-Werte zu.|  
|is_user_process|**bit**|0, wenn es sich um eine Systemsitzung handelt. Andernfalls ist der Wert 1. Lässt keine NULL-Werte zu.|  
|text_size|**int**|TEXTSIZE-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|Sprache|**nvarchar(128)**|LANGUAGE-Einstellung für die Sitzung. Lässt NULL-Werte zu.|  
|date_format|**nvarchar(3)**|DATEFORMAT-Einstellung für die Sitzung. Lässt NULL-Werte zu.|  
|date_first|**smallint**|DATEFIRST-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|quoted_identifier|**bit**|QUOTED_IDENTIFIER-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|arithabort|**bit**|ARITHABORT-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|ansi_null_dflt_on|**bit**|ANSI_NULL_DFLT_ON-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|ansi_defaults|**bit**|ANSI_DEFAULTS-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|ansi_warnings|**bit**|ANSI_WARNINGS-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|ansi_padding|**bit**|ANSI_PADDING-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|ansi_nulls|**bit**|ANSI_NULLS-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|concat_null_yields_null|**bit**|CONCAT_NULL_YIELDS_NULL-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|transaction_isolation_level|**smallint**|Isolationsstufe für Transaktionen der Sitzung.<br /><br /> 0 = Unspecified<br /><br /> 1 = ReadUncomitted<br /><br /> 2 = ReadCommitted<br /><br /> 3 = Repeatable<br /><br /> 4 = Serializable<br /><br /> 5 = Momentaufnahme<br /><br /> Lässt keine NULL-Werte zu.|  
|lock_timeout|**int**|LOCK_TIMEOUT-Einstellung für die Sitzung. Der Wert ist in Millisekunden angegeben. Lässt keine NULL-Werte zu.|  
|deadlock_priority|**int**|DEADLOCK_PRIORITY-Einstellung für die Sitzung. Lässt keine NULL-Werte zu.|  
|row_count|**bigint**|Anzahl der bisher in der Sitzung zurückgegebenen Zeilen. Lässt keine NULL-Werte zu.|  
|prev_error|**int**|ID des letzten in der Sitzung zurückgegebenen Fehlers. Lässt keine NULL-Werte zu.|  
|original_security_id|**varbinary(85)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Sicherheits-ID, die original_login_name zugeordnet ist. Lässt keine NULL-Werte zu.|  
|original_login_name|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename, der vom Client zum Erstellen dieser Sitzung verwendet wurde. Kann ein authentifizierter Anmeldename von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ein authentifizierter Benutzername einer Windows-Domäne oder ein Benutzer einer eigenständigen Datenbank sein. Beachten Sie, dass für die Sitzung nach der ersten Verbindung möglicherweise viele implizite oder explizite Kontextwechsel erfolgt sind. Z. B. wenn [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) verwendet wird. Lässt keine NULL-Werte zu.|  
|last_successful_logon|**datetime**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Zeitpunkt der letzten erfolgreichen Anmeldung für original_login_name, bevor die aktuelle Sitzung gestartet wurde.|  
|last_unsuccessful_logon|**datetime**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Zeitpunkt des letzten nicht erfolgreichen Anmeldeversuchs für original_login_name, bevor die aktuelle Sitzung gestartet wurde.|  
|unsuccessful_logons|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl der nicht erfolgreichen Anmeldeversuche für original_login_name zwischen last_successful_logon und login_time.|  
|group_id|**int**|ID der Arbeitsauslastungsgruppe, zu der diese Sitzung gehört. Lässt keine NULL-Werte zu.|  
|database_id|**smallint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die ID der aktuellen Datenbank für jede Sitzung.|  
|authenticating_database_id|**int**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID der Datenbank, die den Prinzipal authentifiziert. Bei Anmeldungen beträgt der Wert 0. Für Benutzer von eigenständigen Datenbanken ist der Wert die Datenbank-ID der eigenständigen Datenbank.|  
|open_transaction_count|**int**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl der offenen Transaktionen pro Sitzung.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
"Jeder" kann ihre eigenen Sitzungsinformationen zur sehen.  
**[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]:** Erfordert `VIEW SERVER STATE` -Berechtigung für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zu allen Sitzungen auf dem Server finden Sie unter.  
**[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]:** Erfordert `VIEW DATABASE STATE` alle Verbindungen mit der aktuellen Datenbank angezeigt. `VIEW DATABASE STATE`kann nicht gewährt werden, der `master` Datenbank. 
  
  
## <a name="remarks"></a>Hinweise  
 Wenn die **common Criteria-Kompatibilität aktiviert** Serverkonfigurationsoption aktiviert ist, werden die Anmeldestatistiken in den folgenden Spalten angezeigt.  
  
-   last_successful_logon  
  
-   last_unsuccessful_logon  
  
-   unsuccessful_logons  
  
 Ist diese Option nicht aktiviert, geben diese Spalten NULL-Werte zurück. Weitere Informationen zum Festlegen dieser Serverkonfigurationsoption finden Sie unter [common Criteria-Kompatibilität aktiviert (Serverkonfigurationsoption)](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
 
 
 Die Admin-Verbindungen auf Azure SQL-Datenbank werden eine Zeile pro authentifizierter Sitzung angezeigt, während die nichtadministrativen Verbindungen nur Informationen im Zusammenhang mit ihrer Datenbank benutzersitzungen angezeigt werden. 
 
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Für/Anwendung|Beziehung|  
|----------|--------|---------------|------------------|  
|sys.dm_exec_sessions|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|session_id|1:0 oder 1:viele|  
|sys.dm_exec_sessions|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|session_id|1:0 oder 1:viele|  
|sys.dm_exec_sessions|[sys.dm_tran_session_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)|session_id|1:0 oder 1:viele|  
|sys.dm_exec_sessions|[sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)(session_id &#124; 0)|session_id CROSS APPLY<br /><br /> OUTER APPLY|1:0 oder 1:viele|  
|sys.dm_exec_sessions|[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)|session_id|1:1|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-finding-users-that-are-connected-to-the-server"></a>A. Ermitteln der Benutzer, die mit dem Server verbunden sind  
 Im folgenden Beispiel werden die Benutzer ermittelt, die mit dem Server verbunden sind, und die Anzahl der Sitzungen für die einzelnen Benutzer zurückgegeben.  
  
```sql  
SELECT login_name ,COUNT(session_id) AS session_count   
FROM sys.dm_exec_sessions   
GROUP BY login_name;  
```  
  
### <a name="b-finding-long-running-cursors"></a>B. Suchen von Cursorn mit langer Ausführungszeit  
 Im folgenden Beispiel werden die Cursor, die seit einer längeren Zeit als der angegebenen geöffnet sind, die Benutzer, die die Cursor erstellt haben, und die Sitzungen, in denen die Cursor verwendet werden, gesucht.  
  
```sql  
USE master;  
GO  
SELECT creation_time ,cursor_id   
    ,name ,c.session_id ,login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s   
   ON c.session_id = s.session_id   
WHERE DATEDIFF(mi, c.creation_time, GETDATE()) > 5;  
```  
  
### <a name="c-finding-idle-sessions-that-have-open-transactions"></a>C. Suchen von Sitzungen im Leerlauf, für die Transaktionen geöffnet sind  
 Im folgenden Beispiel werden Sitzungen gesucht, für die Transaktionen geöffnet sind und die sich im Leerlauf befinden. Sitzungen, für die derzeit keine Anforderung ausgeführt wird, befinden sich im Leerlauf.  
  
```sql  
SELECT s.*   
FROM sys.dm_exec_sessions AS s  
WHERE EXISTS   
    (  
    SELECT *   
    FROM sys.dm_tran_session_transactions AS t  
    WHERE t.session_id = s.session_id  
    )  
    AND NOT EXISTS   
    (  
    SELECT *   
    FROM sys.dm_exec_requests AS r  
    WHERE r.session_id = s.session_id  
    );  
```  
  
### <a name="d-finding-information-about-a-queries-own-connection"></a>D. Suchen nach Informationen über die eigene Verbindung einer Abfrage  
 Typische Abfrage zum Sammeln von Informationen über die eigene Verbindung einer Abfrage.  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



