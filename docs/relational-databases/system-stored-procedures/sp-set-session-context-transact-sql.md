---
title: Sp_set_session_context (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0cffdacb2ada63ff9c23874795b27f0f5c483adc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsetsessioncontext-transact-sql"></a>Sp_set_session_context (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Legt ein Schlüssel-Wert-Paar im Sitzungskontext fest.  
  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_set_session_context [ @key= ] 'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @key=] 'Key'  
 Der Schlüssel festgelegt wird, vom Typ **Sysname**. Die maximale Schlüsselgröße beträgt 128 Bytes.  
  
 [ @value=] 'Value'  
 Der Wert für den angegebenen Schlüssel des Typs **Sql_variant**. Festlegen eines Werts von NULL gibt den Arbeitsspeicher frei. Die maximale Größe beträgt 8.000 Bytes.  
  
 [ @read_only= ] { 0 | 1 }  
 Ein Kennzeichen vom Typ **Bit**. Bei 1 kann nicht der Wert für den angegebenen Schlüssel erneut auf dieses logische Verbindung geändert werden. Wenn 0 (Standard), wird der Wert geändert werden kann.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer kann einen Sitzungskontext für ihre Sitzung festlegen.  
  
## <a name="remarks"></a>Hinweise  
 Ähnlich wie andere gespeicherten Prozeduren können nur Literale und Variablen (keine Ausdrücke oder Funktionsaufrufe) als Parameter übergeben werden.  
  
 Die Gesamtgröße des Sitzungskontexts ist auf 256 kb beschränkt. Wenn der Satz einen Wert, der bewirkt, dass dieses Limit überschritten wird, schlägt die Anweisung fehl. Sie können überwachen, die gesamtspeicherauslastung in [dm_os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 Sie können die gesamte Speicherverwendung überwachen, indem Sie Abfragen [Sys. dm_os_memory_cache_counters &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) wie folgt: `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie zum Festlegen und dann einen Sitzungen-Kontext-Schlüssel mit dem Namen mit dem Wert der englischen Sprache zurück.  
  
```  
EXEC sp_set_session_context 'language', 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 Das folgende Beispiel veranschaulicht die Verwendung des optionalen nur-Lese Flags.  
  
```  
EXEC sp_set_session_context 'user_id', 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
