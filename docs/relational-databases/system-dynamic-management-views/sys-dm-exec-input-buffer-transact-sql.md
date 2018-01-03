---
title: Sys. dm_exec_input_buffer (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2017
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
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 147ac7627ba30a8a249e00cbf03e37887368de09
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>Sys. dm_exec_input_buffer (Transact-SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Anweisungen, die mit einer Instanz von übermittelt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>Argumente  
*session_id*  
Die Sitzungs-Id wird den Batch gesucht werden soll ausgeführt werden. *Session_id* ist **"smallint"**. *Session_id* kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
Die Request_id von [Sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md). *Request_id* ist **Int**.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|Der Typ des Ereignisses im Eingabepuffer für die angegebene Spid.|  
|**Parameter**|**smallint**|Alle Parameter für die Anweisung bereitgestellt.|  
|**event_info**|**nvarchar(max)**|Der Text der Anweisung im Eingabepuffer für die angegebene Spid.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], wenn der Benutzer die VIEW SERVER STATE-Berechtigung hat, sieht der Benutzer alle zurzeit ausgeführten Sitzungen für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist, andernfalls der Benutzer sieht nur die aktuelle Sitzung.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)], wenn der Benutzer Besitzer der Datenbank ist, sieht der Benutzer alle zurzeit ausgeführten Sitzungen auf die [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ist, andernfalls der Benutzer sieht nur die aktuelle Sitzung.  
  
## <a name="remarks"></a>Hinweise  
 Diese dynamische Verwaltungsfunktion in Verbindung mit Sys. dm_exec_sessions oder Sys. dm_exec_requests verwendet werden kann, durch praktische **CROSS APPLY**.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
 Im folgende Beispiel wird veranschaulicht, eine Sitzungs-Id (SPID) und eine Anforderungs-Id an die Funktion übergeben.  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>B. Mithilfe der versionsübergreifenden gelten für zusätzliche Informationen  
 Im folgende Beispiel werden den Eingabepuffer für Sitzungen mit Sitzungs-Id größer als 50 aufgelistet.  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys. dm_exec_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [Sys. dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
