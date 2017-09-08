---
title: Filegroup_name (Transact-SQL) | Microsoft Docs
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
- FILEGROUP_NAME_TSQL
- FILEGROUP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- displaying filegroup names
- identification numbers [SQL Server], filegroups
- filegroups [SQL Server], IDs
- IDs [SQL Server], filegroups
- FILEGROUP_NAME function
- filegroups [SQL Server], names
- names [SQL Server], filegroups
- viewing filegroup names
ms.assetid: 26add1c0-56e5-47a8-b489-ae56784a7ee9
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3560dc757c9e1f8d6c294f35e69653ba511f96e1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="filegroupname-transact-sql"></a>FILEGROUP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Dateigruppennamen für die angegebene Dateigruppen-Identifikationsnummer (ID) zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FILEGROUP_NAME ( filegroup_id )   
```  
  
## <a name="arguments"></a>Argumente  
 *filegroup_id*  
 Die ID der Dateigruppe, deren Name zurückgegeben werden soll. *Filegroup_id* ist **"smallint"**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **vom Datentyp nvarchar(128)**  
  
## <a name="remarks"></a>Hinweise  
 *Filegroup_id* entspricht der **Data_space_id** Spalte in der **"Sys.FileGroups"** -Katalogsicht angezeigt.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird der Dateigruppenname für die Dateigruppen-ID `1` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
  
SELECT FILEGROUP_NAME(1) AS [Filegroup Name];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Filegroup Name   
-----------------------  
PRIMARY  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
