---
title: Filegroup_id (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILEGROUP_ID_TSQL
- FILEGROUP_ID
dev_langs:
- TSQL
helpviewer_keywords:
- FILEGROUP_ID function
- identification numbers [SQL Server], filegroups
- filegroups [SQL Server], IDs
- IDs [SQL Server], filegroups
- names [SQL Server], filegroups
ms.assetid: 852a76d8-9e61-4a31-84ee-c7edb84a061c
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 714fd89eef4144e2c2a5cd2bba88540cd3ae2d29
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="filegroupid-transact-sql"></a>FILEGROUP_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Dateigruppen-ID für einen angegebenen Dateigruppennamen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FILEGROUP_ID ( 'filegroup_name' )   
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Filegroup_name* **"**  
 Ist ein Ausdruck vom Typ **Sysname** , die den Namen der Dateigruppe, für die die Dateigruppen-ID zurückgegeben darstellt  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 *Filegroup_name* entspricht der **Namen** Spalte in der **"Sys.FileGroups"** -Katalogsicht angezeigt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Dateigruppen-ID für die Dateigruppe mit dem Namen `PRIMARY` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
  
SELECT FILEGROUP_ID('PRIMARY') AS [Filegroup ID];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Filegroup ID  
------------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Filegroup_name &#40; Transact-SQL &#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
