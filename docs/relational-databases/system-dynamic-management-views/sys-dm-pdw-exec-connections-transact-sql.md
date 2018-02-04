---
title: Sys.dm_pdw_exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 201c0fe2d8396d5669f2a05ef43343522827c465
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwexecconnections-transact-sql"></a>sys.dm_pdw_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt Informationen über die zu dieser Instanz von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] hergestellten Verbindungen zurück, sowie Details zu jeder der Verbindungen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|Identifiziert die Sitzung, die dieser Verbindung zugeordnet ist. Verwendung `SESSION_ID()` zurückzugebenden der `session_id` der aktuellen Verbindung.|  
|connect_time|**datetime**|Zeitstempel, der angibt, wann die Verbindung eingerichtet wurde. Lässt keine NULL-Werte zu.|  
|encrypt_option|**nvarchar(40)**|Gibt "true" (Verbindung wird verschlüsselt) oder "false" (Verbindung ist nicht Enctypred).|  
|auth_scheme|**nvarchar(40)**|Gibt das mit dieser Verbindung verwendete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-/Windows-Authentifizierungsschema an. Lässt keine NULL-Werte zu.|  
|client_id|**varchar(48)**|IP-Adresse des Clients eine Verbindung mit diesem Server herstellen. Lässt NULL-Werte zu.|  
|sql_spid|**int**|Die Serverprozess-ID der Verbindung. Verwendung `@@SPID` zurückzugebenden der `sql_spid` der aktuellen Verbindung. Verwenden Sie für die meisten Stammcluster, der `session_id` stattdessen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **VIEW SERVER STATE** Berechtigung auf dem Server.  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions.session_id|dm_pdw_exec_connections.session_id|1:1|  
|dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections.connection_id|n:1|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Typische Abfrage zum Sammeln von Informationen über die eigene Verbindung einer Abfrage.  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

