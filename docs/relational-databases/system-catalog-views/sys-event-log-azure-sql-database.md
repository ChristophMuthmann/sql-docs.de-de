---
title: Sys. event_log (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- event_log
- sys.event_log_TSQL
- event_log_TSQL
- sys.event_log
dev_langs:
- TSQL
helpviewer_keywords:
- event_log
- sys.event_log
ms.assetid: ad5496b5-e5c7-4a18-b5a0-3f985d7c4758
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5d16205902435c3564bc7dc1617a75615e3f1bd9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syseventlog-azure-sql-database"></a>sys.event_log (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt erfolgreiche [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] -Verbindungen, Verbindungsfehlern und Deadlocks. Sie können diese Informationen verwenden, um die Datenbankaktivität mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nachzuverfolgen oder um Fehler zu beheben.  
  
> [!CAUTION]  
>  Für Installationen, die eine große Anzahl von Datenbanken oder großen Anzahl von Anmeldungen kann Aktivitäten in Sys. event_log Einschränkungen bei der Leistung, hohe CPU-Auslastung verursachen und möglicherweise Anmeldefehler zu. Abfragen von Sys. event_log können mit dem Problem beitragen. Microsoft arbeitet daran, um dieses Problem zu beheben. In der Zwischenzeit um die Auswirkungen dieses Problem zu verringern, beschränken Sie Abfragen von Sys. event_log an. Die NewRelic SQL Server-Plug-Ins sollten beim Besuch [Microsoft Azure SQL-Datenbank-Plug-Ins optimieren und Leistung kleiner Anpassungen](https://discuss.newrelic.com/t/microsoft-azure-sql-database-plugin-tuning-performance-tweaks/30729) für Weitere Informationen zur Konfiguration.  
  
 Die `sys.event_log` -Ansicht enthält die folgenden Spalten.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Der Name der Datenbank. Wenn die Verbindung nicht hergestellt werden kann und der Benutzer keinen Datenbanknamen angegeben hat, ist diese Spalte leer.|  
|**start_time**|**datetime2**|UTC-Datum und -Zeit des Beginns des Aggregationsintervalls. Für aggregierte Ereignisse ist die Zeit immer ein Vielfaches von 5 Minuten. Beispiel:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|UTC-Datum und -Zeit des Endes des Aggregationsintervalls. Für aggregierte Ereignisse **End_time** liegt immer genau 5 Minuten später als die entsprechende **Start_time** in derselben Zeile. Für nicht aggregierten Ereignissen entsprechen, **Start_time** und **End_time** gleich der tatsächlichen UTC-Datum und Uhrzeit des Ereignisses.|  
|**event_category**|**nvarchar(64)**|Die Komponente auf hoher Ebene, die dieses Ereignis generiert hat.<br /><br /> Finden Sie unter [Ereignistypen](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) eine Liste der möglichen Werte.|  
|**event_type**|**nvarchar(64)**|Der Typ des Ereignisses.<br /><br /> Finden Sie unter [Ereignistypen](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) eine Liste der möglichen Werte.|  
|**event_subtype**|**int**|Der Untertyp des eintretenden Ereignisses.<br /><br /> Finden Sie unter [Ereignistypen](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) eine Liste der möglichen Werte.|  
|**event_subtype_desc**|**nvarchar(64)**|Die Beschreibung des Ereignisuntertyps.<br /><br /> Finden Sie unter [Ereignistypen](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) eine Liste der möglichen Werte.|  
|**severity**|**int**|Der Schweregrad des Fehlers. Folgende Werte sind möglich:<br /><br /> 0 = Information<br />1 = Warning<br />2 = Fehler|  
|**event_count**|**int**|Die Anzahl, wie oft dieses Ereignis eingetreten ist für die angegebene Datenbank innerhalb des angegebenen Zeitintervalls (**Start_time** und **End_time**).|  
|**description**|**nvarchar(max)**|Detaillierte Beschreibung des Ereignisses.<br /><br /> Finden Sie unter [Ereignistypen](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) eine Liste der möglichen Werte.|  
|**additional_data**|**XML**|*Hinweis: Dieser Wert ist immer NULL für Azure SQL-Datenbank V12. Finden Sie unter [Beispiele](#Deadlock) im Abschnitt zum Abrufen von Deadlockereignisse für V12.*<br /><br /> Für **Deadlock** enthält Ereignisse, diese Spalte das deadlockdiagramm. Bei anderen Ereignistypen enthält diese Spalte NULL. |  
  
##  <a name="EventTypes"></a> Ereignistypen  
 Die von jeder Zeile in dieser Ansicht aufgezeichneten Ereignisse werden nach einer Kategorie identifiziert (**Event_category**), Ereignistyp (**Event_type**), und einen Subtyp (**Event_subtype**). In der folgenden Tabelle werden die Ereignistypen aufgeführt, die in dieser Sicht gesammelt werden.  
  
 Für Ereignisse in der **Konnektivität** Kategorie zusammenfassende Informationen finden Sie in der Sys. database_connection_stats-Sicht.  
  
> [!NOTE]  
>  Diese Sicht enthält nicht alle [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Datenbankereignisse, die eintreten können, sondern nur die hier aufgeführten. Zusätzliche Kategorien, Ereignistypen und Untertypen werden in zukünftigen Versionen von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ggf. hinzugefügt.  
  
|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**description**|  
|-------------------------|---------------------|------------------------|------------------------------|------------------|---------------------|  
|**Konnektivität**|**connection_successful**|0|**connection_successful**|0|Die Verbindung mit der Datenbank war erfolgreich.|  
|**Konnektivität**|**connection_failed**|0|**invalid_login_name**|2|Der Anmeldename ist in dieser SQL Server-Version nicht gültig.|  
|**Konnektivität**|**connection_failed**|1|**windows_auth_not_supported**|2|Windows-Anmeldungen werden in dieser SQL Server-Version nicht unterstützt.|  
|**Konnektivität**|**connection_failed**|2|**attach_db_not_supported**|2|Der Benutzer hat das Anfügen einer Datenbankdatei angefordert, die nicht unterstützt wird.|  
|**Konnektivität**|**connection_failed**|3|**change_password_not_supported**|2|Der Benutzer hat angefordert, das Kennwort des angemeldeten Benutzers zu ändern. Dies wird nicht unterstützt.|  
|**Konnektivität**|**connection_failed**|4|**login_failed_for_user**|2|Fehler bei der Anmeldung für den Benutzer.|  
|**Konnektivität**|**connection_failed**|5|**login_disabled**|2|Die Anmeldung wurde deaktiviert.|  
|**Konnektivität**|**connection_failed**|6|**failed_to_open_db**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Datenbank konnte nicht geöffnet werden. Die Ursache hierfür kann darin liegen, dass die Datenbank nicht vorhanden ist oder keine Authentifizierung zum Öffnen der Datenbank vorhanden ist.|  
|**Konnektivität**|**connection_failed**|7|**blocked_by_firewall**|2|Client-IP-Adresse ist nicht berechtigt, auf den Server zuzugreifen.|  
|**Konnektivität**|**connection_failed**|8|**client_close**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Möglicher Timeout beim Client, als die Verbindung hergestellt wurde. Versuchen Sie, das Verbindungstimeout zu erhöhen.|  
|**Konnektivität**|**connection_failed**|9|**Neukonfiguration**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Verbindungsfehler, da die Datenbank zu diesem Zeitpunkt eine Neukonfiguration durchlaufen hat.|  
|**Konnektivität**|**connection_terminated**|0|**idle_connection_timeout**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Verbindung ist länger im Leerlauf, als der vom System definierte Schwellenwert angibt.|  
|**Konnektivität**|**connection_terminated**|1|**Neukonfiguration**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Sitzung wurde aufgrund einer Neukonfiguration der Datenbank beendet.|  
|**Konnektivität**|**Einschränkung**|*\<Ursachencode >*|**reason_code**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Anforderung wird gedrosselt.  Ursachencode:  *\<Ursachencode >*. Weitere Informationen finden Sie unter [Moduleinschränkung](http://msdn.microsoft.com/library/windowsazure/dn338079.aspx).|  
|**Konnektivität**|**throttling_long_transaction**|40549|**long_transaction**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Sitzung wird aufgrund einer Transaktion mit langer Laufzeit beendet. Verkürzen Sie die Transaktion. Weitere Informationen finden Sie unter [Ressourcengrenzwerte](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**Konnektivität**|**throttling_long_transaction**|40550|**excessive_lock_usage**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Sitzung wurde beendet, da zu viele Sperren abgerufen wurden. Reduzieren Sie die Anzahl der in einer einzelnen Transaktion gelesenen oder geänderten Zeilen. Weitere Informationen finden Sie unter [Ressourcengrenzwerte](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**Konnektivität**|**throttling_long_transaction**|40551|**excessive_tempdb_usage**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Sitzung wurde aufgrund übermäßiger TEMPDB-Auslastung beendet. Ändern Sie die Abfrage, um die Verwendung des temporären Tabellenbereichs zu verringern. Weitere Informationen finden Sie unter [Ressourcengrenzwerte](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**Konnektivität**|**throttling_long_transaction**|40552|**excessive_log_space_usage**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Sitzung wurde aufgrund übermäßiger Verwendung des Speicherplatzes für das Transaktionsprotokoll beendet. Reduzieren Sie die Anzahl der in einer einzelnen Transaktion geänderten Zeilen. Weitere Informationen finden Sie unter [Ressourcengrenzwerte](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**Konnektivität**|**throttling_long_transaction**|40553|**excessive_memory_usage**|2|*Hinweis: Gilt nur für Azure SQL-Datenbank V11.*<br /><br /> Die Sitzung wurde aufgrund übermäßiger Speicherauslastung beendet. Ändern Sie die Abfrage, damit weniger Zeilen verarbeitet werden. Weitere Informationen finden Sie unter [Ressourcengrenzwerte](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx).|  
|**Datenbankmodul**|**Deadlock**|0|**Deadlock**|2|Deadlock ist aufgetreten.|  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer mit Berechtigung zum Zugriff auf die **master** Datenbank haben schreibgeschützten Zugriff auf diese Sicht.  
  
## <a name="remarks"></a>Hinweise  
  
### <a name="event-aggregation"></a>Ereignisaggregation  
 Die Ereignisinformationen für diese Sicht werden gesammelt und innerhalb von 5-minütigen Intervallen aggregiert. Die **Event_count** Spalte dar, wie oft ein bestimmter **Event_type** und **Event_subtype** für eine bestimmte Datenbank innerhalb eines angegebenen Zeitintervalls aufgetreten.  
  
> [!NOTE]  
>  Einige Ereignisse wie Deadlocks werden nicht aggregiert. Für diese Ereignisse **Event_count** 1 und **Start_time** und **End_time** ist gleich der tatsächlichen UTC-Datum und Uhrzeit des Auftretens des Ereignisses.  
  
 Wenn ein Benutzer zum Beispiel aufgrund eines ungültigen Anmeldenamens sieben Mal zwischen 11:00 und 11:05 Uhr am 05.02.2012 (UTC) keine Verbindung mit der Datenbank Database1 herstellen kann, sind diese Informationen in dieser Sicht in einer einzelnen Zeile verfügbar:  
  
|**database_name**|**start_time**|**end_time**|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**event_count**|**description**|**additional_data**|  
|------------------------|---------------------|-------------------|-------------------------|---------------------|------------------------|------------------------------|------------------|----------------------|---------------------|--------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`connectivity`|`connection_failed`|`4`|`login_failed_for_user`|`2`|`7`|`Login failed for user.`|`NULL`|  
  
### <a name="interval-starttime-and-endtime"></a>
          start_time und end_time des Intervalls  
 Ein Ereignis wird in ein aggregationsintervall eingeschlossen, wenn das Ereignis tritt auf, *auf* oder *nach *** Start_time** und *vor *** End_time** für dieses Intervall. Beispielsweise würde ein Ereignis, das genau zum Zeitpunkt `2012-10-30 19:25:00.0000000` eintritt, nur im zweiten unten gezeigten Intervall aufgenommen werden:  
  
```  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>Datenupdates  
 Die Daten in dieser Sicht werden im Zeitverlauf gesammelt. Normalerweise werden die Daten innerhalb einer Stunde nach Beginn des Aggregationsintervalls gesammelt, es kann aber maximal 24 Stunden dauern, bis alle Daten in der Sicht angezeigt werden. Während dieser Zeit werden die Informationen in einer einzelnen Zeile möglicherweise gelegentlich aktualisiert.  
  
### <a name="data-retention"></a>Datenbeibehaltung  
 Die Daten in dieser Sicht werden maximal 30 Tage oder kürzer beibehalten, abhängig von der Anzahl der Datenbanken auf dem logischen Server und der Anzahl der eindeutigen Ereignisse, die jede Datenbank generiert. Um diese Informationen für einen längeren Zeitraum beizubehalten, kopieren Sie die Daten in eine separate Datenbank. Nachdem Sie eine erste Kopie der Sicht erstellt haben, werden die Zeilen in der Sicht möglicherweise aktualisiert, während die Daten gesammelt werden. Damit die Kopie der Daten aktuell bleibt, führen Sie regelmäßig einen Tabellenscan der Zeilen aus, um nach einer Erhöhung der Ereignisanzahl für vorhandene Zeilen zu suchen und um neue Zeilen zu ermitteln (eindeutige Zeilen bestimmen Sie anhand der Start- und Endzeiten). Aktualisieren Sie dann die Kopie der Daten mit diesen Änderungen.  
  
### <a name="errors-not-included"></a>Fehler nicht enthalten  
 Diese Sicht enthält möglicherweise nicht alle Verbindungs- und Fehlerinformationen:  
  
-   Diese Ansicht enthält nicht alle [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Datenbankfehler, die eintreten können, sondern nur die unter [Ereignistypen](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) in diesem Thema.  
  
-   Wenn ein Computerfehler innerhalb des [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Datencenters auftritt, ist es möglich, dass eine geringe Anzahl der Daten des logischen Servers in der Ereignistabelle fehlt.  
  
-   Wenn eine IP-Adresse von DoSGuard blockiert wurde, können Verbindungsversuchsereignisse von dieser IP-Adresse nicht gesammelt werden. Diese werden in dieser Sicht nicht angezeigt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="simple-examples"></a>Einfache Beispiele  
 Die folgende Abfrage gibt alle Ereignisse zurück, die zwischen 12 Uhr mittags am 25.09.2011 und 12 Uhr mittags am 28.09.2011 (UTC) eingetreten sind. Standardmäßig werden Abfrageergebnisse sortiert, durch **Start_time** (in aufsteigender Reihenfolge).  
  
```  
SELECT * FROM sys.event_log   
WHERE start_time >= '2011-09-25:12:00:00'   
    AND end_time <= '2011-09-28 12:00:00';  
```  
  
 Die folgende Abfrage gibt alle Deadlockereignisse für die Datenbank Database1 (gilt nur für Azure SQL-Datenbank V11) zurück.  
  
```  
SELECT * FROM sys.event_log   
WHERE event_type = 'deadlock'   
    AND database_name = 'Database1';  
```  
<a name="Deadlock"></a> Die folgende Abfrage gibt alle Deadlockereignisse für die Datenbank Database1 (gilt nur für Azure SQL-Datenbank V12).  
  
```  
WITH CTE AS (  
       SELECT CAST(event_data AS XML)  AS [target_data_XML]   
   FROM sys.fn_xe_telemetry_blob_target_read_file('dl', null, null, null)  
)  
SELECT target_data_XML.value('(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
target_data_XML.query('/event/data[@name=''xml_report'']/value/deadlock') AS deadlock_xml,  
target_data_XML.query('/event/data[@name=''database_name'']/value').value('(/value)[1]', 'nvarchar(100)') AS db_name  
FROM CTE   
  
```  
  
  
 Die folgende Abfrage gibt harte Drosselungen für SQL-Arbeitsthreadereignisse zurück, die zwischen 10:00 und 11:00 Uhr am 25.09.2011 (UTC) eingetreten sind.  
  
```  
SELECT * FROM sys.event_log   
WHERE event_type = 'throttling'   
    AND event_subtype = 4194307   
    AND start_time >= '2011-09-25 10:00:00'   
    AND end_time <= '2011-09-25 11:00:00';  
```  
  
### <a name="db-scoped-extended-event"></a>DB-Gültigkeitsbereich erweiterte Ereignisse  
 Verwenden Sie den folgenden Beispielcode zum Einrichten der Sitzungs für die Db-Gültigkeitsbereich erweiterte Ereignisse (XEvent):  
  
```sql  
IF EXISTS  
    (SELECT * from sys.database_event_sessions  
        WHERE name = 'azure_monitor_deadlock_session')  
BEGIN  
    ALTER EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE  
        DROP TARGET package0.ring_buffer;  
  
    DROP EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE;  
END  
  
CREATE EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    ADD EVENT sqlserver.database_xml_deadlock_report  
    ADD TARGET package0.ring_buffer  
    (  
        SET max_memory = 2048, max_events_limit = 10  
    )  
    WITH (STARTUP_STATE = ON,  
          EVENT_RETENTION_MODE = ALLOW_SINGLE_EVENT_LOSS);  
  
ALTER EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    STATE = START;  
```  
  
### <a name="check-for-deadlock"></a>Kontrollkästchen für Deadlocks

Verwenden Sie die folgende Abfrage überprüft, ob ein Deadlock vorhanden ist.  
  
```sql  
WITH CTE AS (  
    SELECT CAST(xet.target_data AS XML)  AS [target_data_XML]  
        FROM            sys.dm_xe_database_session_targets AS xet  
             INNER JOIN sys.dm_xe_database_sessions        AS xe  
                 ON (xe.address = xet.event_session_address)  
        WHERE xe.name = 'azure_monitor_deadlock_session'  
)  
, CTE2 AS (  
    SELECT  
            T2.EventData.query('.').value(  
                '(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
            T2.EventData.query('.').query(  
                '(/event/data/value/deadlock)[1]')     AS deadlock_xml  
        FROM CTE  
            CROSS Apply [target_data_XML].nodes(  
                '/RingBufferTarget/event') AS T2(EventData)  
)  
SELECT * FROM CTE2;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse in Azure SQL-Datenbank](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
  
  
