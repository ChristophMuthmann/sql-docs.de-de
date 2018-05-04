---
title: sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 6794e073-0895-4507-aba3-c3545acc843f
caps.latest.revision: 9
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6680957164eb494600fece4df5dddbae36ef4c0e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnstmtsqlhandlefromsqlstmt-transact-sql"></a>sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ruft die **Stmt_sql_handle** für eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung unter angegebenen Parametrisierung (einfache oder erzwungene). Dadurch können Sie zum Verweisen auf Abfragen im Abfragespeicher gespeichert sind, mit deren **Stmt_sql_handle** kennen, deren Text.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.fn_stmt_sql_handle_from_sql_stmt   
(  
    'query_sql_text',   
    [ query_param_type   
) [;]  
```  
  
## <a name="arguments"></a>Argumente  
 *query_sql_text*  
 Ist der Text der Abfrage im Abfragespeicher, dem das Handle des werden sollen. *Query_sql_text* ist ein **nvarchar(max)**, hat keinen Standardwert.  
  
 *query_param_type*  
 Ist der Parametertyp der Abfrage. *Query_param_type* ist ein **"tinyint"**. Folgende Werte sind möglich:  
  
-   NULL – der Standardwert ist 0  
  
-   0 – keine  
  
-   1 – Benutzer  
  
-   2 – einfach  
  
-   3 – erzwungen  
  
## <a name="columns-returned"></a>Zurückgegebene Spalten  
 Die folgende Tabelle enthält die Spalten dieser sys.fn_stmt_sql_handle_from_sql_stmt zurückgibt.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|**statement_sql_handle**|**varbinary(64)**|Das SQL-Handle.|  
|**query_sql_text**|**nvarchar(max)**|Der Text, der die [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.|  
|**query_parameterization_type**|**tinyint**|Der Typ des Abfrage-Parametrisierung.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **EXECUTE** Berechtigung für die Datenbank und **löschen** -Berechtigung für die Abfrage Katalogsichten des Abfragespeichers.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel führt eine Anweisung aus und verwendet dann `sys.fn_stmt_sql_handle_from_sql_stmt` das SQL-Handle der Anweisung zurückgegeben.  
  
```  
SELECT * FROM sys.databases;   
SELECT * FROM sys.fn_stmt_sql_handle_from_sql_stmt('SELECT * FROM sys.databases', NULL);  
```  
  
 Verwenden Sie die Funktion zum Korrelieren der abfragespeicherdaten mit anderen dynamischen Verwaltungssichten. Im folgenden Beispiel:  
  
```  
SELECT qt.query_text_id, q.query_id, qt.query_sql_text, qt.statement_sql_handle,  
q.context_settings_id, qs.statement_context_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_id  
CROSS APPLY sys.fn_stmt_sql_handle_from_sql_stmt (qt.query_sql_text, null) AS fn_handle_from_stmt  
JOIN sys.dm_exec_query_stats AS qs   
    ON fn_handle_from_stmt.statement_sql_handle = qs.statement_sql_handle;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [Sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
