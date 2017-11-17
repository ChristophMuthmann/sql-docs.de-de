---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2a0d500a-f6c8-490f-9abd-3ae824986404
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9089c21109d6eedb1cdae0082e1530e8d77d9dde
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt die ID des aktuellen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] Sitzung.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **nvarchar(32)** Wert.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die Sitzungs-ID wird jeder benutzerverbindung zugewiesen, wenn die Verbindung hergestellt wird. Es bleibt für die Dauer der Verbindung. Wenn die Verbindung beendet wird, wird die Sitzungs-ID freigegeben.  
  
 Die Sitzungs-ID beginnt mit dem Buchstaben "SID". Diese Groß-/Kleinschreibung beachtet und muss groß geschrieben werden, wenn die Sitzungs-ID verwendet wird, in [!INCLUDE[DWsql](../../includes/dwsql-md.md)] Befehle.  
  
 Sie können die Sicht Abfragen [sys.dm_pdw_exec_sessions](http://msdn.microsoft.com/en-us/5b656c55-427f-4306-8bd9-9d7987c203d9) die gleiche Informationen wie diese Funktion abrufen.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die ID der aktuellen Sitzung.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Db_name &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40; SQL Datawarehouse &#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  

