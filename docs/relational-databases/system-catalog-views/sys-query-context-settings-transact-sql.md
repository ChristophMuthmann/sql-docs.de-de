---
title: Sys.query_context_settings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2016
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
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9be8b645cf0a5f08132110dd1eca43c19726d75a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysquerycontextsettings-transact-sql"></a>Sys.query_context_settings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Enthält Informationen über die Semantik beeinflussen Kontext Einstellungen im Zusammenhang mit einer Abfrage. Es stehen eine Reihe von Kontext Einstellungen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die die Semantik der Abfrage (definieren das richtige Ergebnis der Abfrage) beeinflussen. Derselbe Abfragetext, kompiliert mit unterschiedlichen Einstellungen erzeugen möglicherweise unterschiedliche Ergebnisse (abhängig von den zugrunde liegenden Daten).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|Der Primärschlüssel. Dieser Wert wird für Abfragen in Showplan XML verfügbar gemacht.|  
|**Set_Options**|**varbinary(8)**|Bitmaske, die Darstellung des Status von mehrere SET-Optionen. Weitere Informationen finden Sie unter [dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).|  
|**language_id**|**smallint**|Die Id der Sprache. Weitere Informationen finden Sie unter [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|**date_format**|**smallint**|Das Datumsformat. Weitere Informationen finden Sie unter [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|Der erste Date-Wert. Weitere Informationen finden Sie unter [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary(2)**|Bitmaske-Feld, das zeigt Typ der Abfrage oder Kontext, in dem Abfrage ausgeführt wurde. <br />Spaltenwert kann die Kombination mehrerer Flags (im Hexadezimalformat ausgedrückt):<br /><br /> 0 x 0 – reguläre Abfrage (keine bestimmte Flags)<br /><br /> 0 x 1 - Abfrage, die über eine der Cursor APIs, die gespeicherten Prozeduren ausgeführt wurde<br /><br /> 0 x 2 – Abfrage für die Benachrichtigung<br /><br /> 0 x 4 – interne Abfrage<br /><br /> 0 x 8 – automatisch parametrisierten Abfrage ohne universal Parametrisierung<br /><br /> 0 x 10 – Cursor-Fetch Abfrage aktualisieren<br /><br /> 0 x 20 - Abfrage, die Anforderungen zum Aktualisieren von Cursor verwendet wird<br /><br /> 0 x 40 - erste Resultset wird zurückgegeben, wenn ein Cursor geöffnet wird (Cursor Fetch automatisch)<br /><br /> 0 x 80 – verschlüsselte Abfrage<br /><br /> 0 x 100-Abfrage im Kontext der Sicherheit auf Zeilenebene Prädikat|  
|**required_cursor_options**|**int**|Vom Benutzer angegebene Cursoroptionen, z. B. der Cursortyp.|  
|**acceptable_cursor_options**|**int**|Cursoroptionen, in die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine implizite Konvertierung vorgenommen werden kann, um die Ausführung der Anweisung zu unterstützen.|  
|**merge_action_type**|**smallint**|Der Typ des triggerausführungsplans, die als Ergebnis verwendet eine **MERGE** Anweisung.<br /><br /> 0 gibt an, eine nicht-triggerplan an, einen triggerplan, der nicht als Ergebnis ausgeführt wird eine **MERGE** -Anweisung oder einen triggerplan, der als Ergebnis führt eine **MERGE** -Anweisung, die nur eine an**Löschen** Aktion.<br /><br /> 1 gibt an, ein **einfügen** -triggerplan an, die als Ergebnis führt eine **MERGE** Anweisung.<br /><br /> 2 Gibt an, eine **UPDATE** -triggerplan an, die als Ergebnis führt eine **MERGE** Anweisung.<br /><br /> 3 gibt eine **löschen** -triggerplan an, die als Ergebnis ausgeführt wird eine **MERGE** -Anweisung mit einer entsprechenden **einfügen** oder **UPDATE** Aktion.<br /><br /> <br /><br /> Auf geschachtelte Trigger, die durch kaskadierende Aktionen ausgeführt werden, ist dieser Wert die Aktion der **MERGE** -Anweisung, die das Kaskadieren verursacht wurde.|  
|**default_schema_id**|**int**|Die ID des Standardschemas, die verwendet wird, zum Auflösen von Namen, die nicht vollqualifiziert sind.|  
|**is_replication_specific**|**bit**|Für die Replikation verwendet.|  
|**is_contained**|**varbinary(1)**|1 gibt an, eine eigenständige Datenbank.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW DATABASE STATE** Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [Sys. query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [Sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [Sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
