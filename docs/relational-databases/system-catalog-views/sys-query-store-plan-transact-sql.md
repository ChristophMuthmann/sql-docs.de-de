---
title: Sys. query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0950cf33d112d299de615a702d0fbac7cbfdc0e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreplan-transact-sql"></a>Sys. query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Enthält Informationen zu jeder Ausführungsplan einer Abfrage zugeordnet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**"Plan_id"**|**bigint**|Der Primärschlüssel.|  
|**"query_id"**|**bigint**|Fremdschlüssel. Verknüpft mit [query_store_query &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|Die ID der Gruppe "Plan". Cursorabfragen erfordern in der Regel mehrere (füllen und fetch) Pläne. Füllen und Fetch-Pläne, die zusammen kompiliert werden, die in der gleichen Gruppe sind.<br /><br /> 0 bedeutet, dass der Plan nicht in einer Gruppe ist.|  
|**ENGINE_VERSION**|**nvarchar(32)**|Version des Moduls verwendet, um den Plan zu kompilieren **"major.minor.build.revision"** Format.|  
|**COMPATIBILITY_LEVEL**|**smallint**|Datenbank-Kompatibilitätsgrad der Datenbank in der Abfrage verwiesen wird.|  
|**query_plan_hash**|**Binary(8)**|MD5-Hash des einzelnen Plans.|  
|**query_plan**|**nvarchar(max)**|Showplan XML für den Abfrageplan.|  
|**is_online_index_plan**|**bit**|Plan wurde während einer onlineindexerstellung verwendet.|  
|**is_trivial_plan**|**bit**|Plan ist eine triviale Plan (Ausgabe in die Stufe 0 des Abfrageoptimierers).|  
|**is_parallel_plan**|**bit**|Plan ist parallel.|  
|**is_forced_plan**|**bit**|Plan wird als erzwungen, wenn der Benutzer die gespeicherte Prozedur führt markiert **sys.sp_query_store_force_plan**. Nutzungsplanerzwingungsmechanismus *garantiert nicht* dieser genau dieses Plans für die Abfrage verweist verwendet **"query_id"**. Das Erzwingen eines Plans bewirkt, dass die Abfrage erneut kompiliert werden und in der Regel erzeugt genau die gleichen oder ähnlichen Plan für den Plan verweist **"Plan_id"**. Wenn das Erzwingen eines Plans nicht gelingt, **Force_failure_count** wird erhöht und **Last_force_failure_reason** wird mit der Fehlerursache aufgefüllt.|  
|**is_natively_compiled**|**bit**|Plan enthält Speicheroptimierte systemintern kompilierte Prozeduren. (0 = FALSE, 1 = "TRUE").|  
|**force_failure_count**|**bigint**|Anzahl der Fälle, in denen dieser Plan erzwingen fehlgeschlagen ist. Er kann nur verwendet werden, wenn die Abfrage neu kompiliert wird erhöht werden (*nicht bei jeder Ausführung*). Er auf 0 zurückgesetzt wird jedes Mal **Is_plan_forced** von geändert wird **"false"** auf **"true"**.|  
|**last_force_failure_reason**|**int**|Grund, warum das Erzwingen eines Plans fehlgeschlagen ist.<br /><br /> 0: keine Fehler, die andernfalls Fehlernummer des Fehlers, der verursacht hat, die durch das Erzwingen des fehlschlägt<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIMEOUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<anderer Wert >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**vom Datentyp nvarchar(128)**|Die textbeschreibung des Last_force_failure_reason_desc.<br /><br /> ONLINE_INDEX_BUILD: Abfrage versucht, Daten zu ändern, während die Zieltabelle einen Index verfügt, der online erstellt wird<br /><br /> INVALID_STARJOIN: Plan enthält ungültige Spezifikation der StarJoin<br /><br /> Timeout: Optimierer überschritten Anzahl zulässiger Vorgänge bei der Suche nach Plan, gemäß der erzwungenen Plans<br /><br /> NO_DB: Eine Datenbank angegeben, die im Plan ist nicht vorhanden.<br /><br /> HINT_CONFLICT: Abfrage kann nicht kompiliert werden, da der Plan mit einem Abfragehinweis steht in Konflikt<br /><br /> DQ_NO_FORCING_SUPPORTED: Abfrage kann nicht ausgeführt werden, da der Plan durch Verwendung einer verteilten Abfrage oder volltextvorgängen steht in Konflikt.<br /><br /> NO_PLAN: Abfrageprozessor konnte keinen Abfrageplan erstellen da erzwungener Plan nicht verifiziert werden konnte, für die Abfrage gültig ist<br /><br /> NO_INDEX: Index angegeben im Plan nicht mehr vorhanden ist.<br /><br /> VIEW_COMPILE_FAILED: Konnte wegen eines Problems in einer indizierten Sicht verwiesen wird, im Plan Abfrageplan nicht erzwungen werden.<br /><br /> GENERAL_FAILURE: Allgemeine erzwingen Fehler (nicht mit den oben genannten Gründen behandelt)|  
|**count_compiles**|**bigint**|Planen Sie die Kompilierung Statistiken.|  
|**initial_compile_start_time**|**datetimeoffset**|Planen Sie die Kompilierung Statistiken.|  
|**last_compile_start_time**|**datetimeoffset**|Planen Sie die Kompilierung Statistiken.|  
|**last_execution_time**|**datetimeoffset**|Zeitpunkt der letzten Ausführung bezieht sich auf die letzte Endzeit des Abfrageplans /.|  
|**avg_compile_duration**|**float**|Planen Sie die Kompilierung Statistiken.|  
|**last_compile_duration**|**bigint**|Planen Sie die Kompilierung Statistiken.|  
  
## <a name="plan-forcing-limitations"></a>Einschränkungen für die planerzwingung
Der Abfragedatenspeicher verfügt über eine Mechanismus, der den Abfrageoptimierer dazu zwingen kann, einen bestimmten Ausführungsplan zu verwenden. Es gibt allerdings Einschränkungen, die dazu führen können, dass das Erzwingen eines Plans verhindert wird. 

Erstens, wenn der Plan die folgenden Konstruktionen enthält:
* INSERT BULK-Anweisung
* INSERT BULK-Anweisung
* einen Verweis auf eine externe Tabelle
* eine verteilte Abfrage oder Volltextvorgänge
* globale Abfragen 
* Cursor
* eine ungültige Sternverknüpfungsspezifikation 

Zweitens, wenn Objekte, die der Plan verwendet, nicht mehr zur Verfügung stehen:
* eine Datenbank (wenn die Datenbank, aus der der Plan kommt, nicht mehr existiert)
* ein Index (nicht mehr vorhanden oder deaktiviert)

Und drittens, bei Problemen mit dem Plan selbst:
* Er darf nicht abgefragt werden.
* Der Abfrageoptimierer hat die Zahl an zulässigen Vorgängen überschritten.
* Die XML des Plans ist ungültig formuliert.

## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW DATABASE STATE** Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_query &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [Sys.query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [Sys. query_store_runtime_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Der Abfragespeicher gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
