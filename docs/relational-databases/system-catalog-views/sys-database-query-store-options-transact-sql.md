---
title: database_query_store_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1c048c66e20e210f84d26dbff492aede56839fe2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt die Optionen zum Abfragespeicher für diese Datenbank zurück.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|Gibt den gewünschten Betriebsmodus des Abfragespeichers, die explizit vom Benutzer festgelegten an.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(64)**|Textbeschreibung für den gewünschten Betriebsmodus des Abfragespeichers:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|Gibt den Betriebsmodus des Abfragespeichers an. Zusätzlich zur Liste der gewünschte Zustände seitens des Benutzers erforderlich kann die tatsächlichen Status Status "Fehler" sein.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = FEHLER|  
|**actual_state_desc**|**nvarchar(64)**|Die textbeschreibung der tatsächlichen Betriebsmodus des Abfragespeichers.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> Es gibt Situationen, wenn der tatsächliche Zustand vom gewünschten Zustand abweicht:<br /><br /> Der Abfragespeicher kann im Nur-Lese-Modus ausgeführt werden, selbst wenn Lese-/ Schreibzugriff, die vom Benutzer angegeben wurde. Beispielsweise kann, die auftreten, wenn die Datenbank im schreibgeschützten Modus befindet oder wenn die Größe des Abfragespeichers das Kontingent überschritten.<br /><br /> Sehr seltenen Fällen kann der Abfragespeicher im Status "Fehler" aufgrund von internen Fehlern annehmen. In diesem Fall konnte der Abfragespeicher wiederhergestellt werden, durch das Ausführen **Sp_query_store_consistency_check** gespeicherte Prozedur in der betroffenen Datenbank.|  
|**readonly_reason**|**int**|Wenn die **Desired_state_desc** ist READ_WRITE und **Actual_state_desc** ist READ_ONLY, **"readonly_reason"** gibt etwas angeben, warum der Abfragespeicher im zuordnen Schreibgeschützter Modus.<br /><br /> 1-Datenbank befindet sich im Nur-Lese-Modus<br /><br /> 2 – Datenbank befindet sich im Einzelbenutzermodus<br /><br /> 4 – Datenbank befindet sich im Notfallmodus<br /><br /> 8 – die Datenbank ist sekundären Replikat (gilt für Always On und Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Geo-Replikation). Dieser Wert kann nur auf effektiv beobachtet werden **lesbare** sekundäre Replikate<br /><br /> 65536: der Abfragespeicher hat die maximale Größe festlegen, indem die Option MAX_STORAGE_SIZE_MB erreicht.<br /><br /> 131072 – die Anzahl der anderen Anweisungen im Abfragespeicher hat die internen Speicher erreicht. Erwägen Sie, entfernen Sie Abfragen, die Sie nicht benötigen, oder ein Upgrade auf eine höhere Dienstebene So aktivieren Sie Abfragespeicher in Lese-/ Schreibmodus übertragen.<br />Gilt nur für [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> 262144 – Größe des speicherinternen-Elemente, die darauf warten, auf dem Datenträger beibehalten werden, hat die internen Speicher-Limit erreicht. Der Abfragespeicher wird nur-Lese-Modus vorübergehend, bis der in-Memory-Elemente auf dem Datenträger beibehalten werden. <br />Gilt nur für [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br />524288 – die Datenbank hat die datenträgergrößenbegrenzung erreicht. Der Abfragespeicher ist Teil Benutzerdatenbank, damit es ist nicht mehr verfügbaren Speicherplatz für eine Datenbank, die bedeutet, dass der Abfragespeicher weiter anwächst kann nicht mehr.<br />Gilt nur für [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. <br /> <br /> So wechseln Sie den Abfragespeicher Vorgänge Modus wieder zum Lese-/ Schreibzugriff finden Sie unter **überprüfen Sie, ob der Abfragespeicher kontinuierlich Abfragedaten erfasst ist** Abschnitt [bewährte Methoden für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md).|  
|**current_storage_size_mb**|**bigint**|Die Größe des Abfragespeichers auf dem Datenträger in Megabyte.|  
|**flush_interval_seconds**|**bigint**|Legt fest, für die reguläre der abfragespeicherdaten auf einem Datenträger gespeichert. Standardwert ist 900 (15 Min.).<br /><br /> Ändern Sie mithilfe der `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` Anweisung.|  
|**interval_length_minutes**|**bigint**|Statistiken aggregationsintervalls. Beliebige Werte sind nicht zulässig. Verwenden Sie eine der folgenden: 1, 5, 10, 15, 30, 60 und 1440 Minuten. Der Standardwert ist 60 Minuten.|  
|**max_storage_size_mb**|**bigint**|Maximale Datenträgergröße für den Abfragespeicher. Standardwert ist 100 MB.<br />Der Standardwert für die Premium Edition von [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] liegt bei 1 GB, für die Basic Edition von [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] bei 10 MB.<br /><br /> Ändern Sie mithilfe der `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` Anweisung.|  
|**stale_query_threshold_days**|**bigint**|Anzahl der Tage, die keine Richtlinieneinstellungen Abfragen im Abfragespeicher beibehalten werden. Standardwert ist 30. Auf 0 festgelegt, um die Aufbewahrungsrichtlinie zu deaktivieren.<br />Für die Basic-Edition von [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ist der Standardwert 7 Tage.<br /><br /> Ändern Sie mithilfe der `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` Anweisung.|  
|**max_plans_per_query**|**bigint**|Schränkt die maximale Anzahl von gespeicherten Pläne an. Standardwert ist 200. Wenn der Höchstwert erreicht ist, beendet der Abfragespeicher die Erfassung nach neue Pläne für diese Abfrage. Auf 0 festlegen, wird die Einschränkung im Hinblick auf die Anzahl der erfassten Pläne entfernt.<br /><br /> Ändern Sie mithilfe der `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` Anweisung.|  
|**query_capture_mode**|**smallint**|Die derzeit aktiven abfrageerfassungsmodus:<br /><br /> 1 = ALL: alle Abfragen werden erfasst. Dies ist der Standardwert für die Konfiguration für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = die AUTO - Capture relevanten Abfragen basierend auf der Anzahl und dem Ressourcenverbrauch Ausführung. Dies ist der Standardwert für die Konfiguration für [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].<br /><br /> 3 = keine - Erfassung neuer Abfragen beendet. Der Abfragedatenspeicher sammelt weiterhin Statistiken zur Kompilierung und Runtime für Abfragen, die bereits erfasst wurden. Verwenden Sie diese Konfiguration mit Vorsicht, da übersehen werden können, um wichtige Abfragen zu erfassen.|  
|**query_capture_mode_desc**|**nvarchar(60)**|Die textbeschreibung der tatsächlichen Aufzeichnungsmodus des Abfragespeichers:<br /><br /> Alle (Standard für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> AUTOMATISCH (Standard für [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> Keine|  
|**size_based_cleanup_mode**|**smallint**|Steuert, ob die Bereinigung automatisch aktiviert wird, wenn sich die Gesamtmenge der Daten der maximalen Größe nähert:<br /><br /> 1 = OFF – Größe basierend die Bereinigung nicht automatisch aktiviert.<br /><br /> 2 = die AUTO - Größe basierend die Bereinigung wird automatisch aktiviert, wenn auf den Datenträger erreicht 90 % der Größe **Max_storage_size_mb**. Dies ist der Standardkonfigurationswert.<br /><br />Ein auf der Größe basierendes Cleanup entfernt die am wenigsten aufwendigen und die ältesten Abfragen. Es wird bei ca. 80 % des Max_storage_size_mb beendet.|  
|**size_based_cleanup_mode_desc**|**smallint**|Die textbeschreibung des tatsächlichen größenbasierte Cleanup-Modus des Abfragespeichers:<br /><br /> OFF <br /><br /> AUTO (Standardeinstellung)|  
|**wait_stats_capture_mode**|**smallint**|Steuert, ob der Abfragespeicher Erfassung von wartestatistik ausführt: <br /><br /> 0 = OFF <br /><br /> 1 = ON<br /> **Gilt für**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|**wait_stats_mode_capture_desc**|**nvarchar(60)**|Die textbeschreibung des Aufzeichnungsmodus die tatsächliche Wartezeit-Statistiken: <br /><br /> OFF <br /><br /> (Standard)<br /> **Gilt für**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW DATABASE STATE** Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [Sys. query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [Gespeicherte Prozeduren den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
