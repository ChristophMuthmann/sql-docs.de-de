---
title: SESSION_ID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ed9b2ccee7c9eb05def55514f1131dd7251a59b0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt die ID der aktuellen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]- oder [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]-Sitzung zurück.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt einen **nvarchar(32)**-Wert zurück.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die Sitzungs-ID wird jeder Benutzerverbindung beim Herstellen der Verbindung zugewiesen und bleibt für die Dauer der Verbindung bestehen. Wenn die Verbindung beendet wird, wird die Sitzungs-ID freigegeben.  
  
 Die Sitzungs-ID beginnt mit den Buchstaben „SID“. Für diese muss die Groß-/Kleinschreibung beachtet werden. Außerdem müssen sie groß geschrieben werden, wenn die Sitzungs-ID in [!INCLUDE[DWsql](../../includes/dwsql-md.md)]-Befehlen verwendet wird.  
  
 Sie können die Sicht [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) abfragen, um dieselben Informationen wie diese Funktion abzurufen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die ID der aktuellen Sitzung zurückgegeben.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
