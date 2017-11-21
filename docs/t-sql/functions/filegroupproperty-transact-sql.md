---
title: FILEGROUPPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILEGROUPPROPERTY_TSQL
- FILEGROUPPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], property values
- FILEGROUPPROPERTY function
- viewing filegroup properties
- displaying filegroup properties
ms.assetid: b3a930e6-df05-4034-929c-f681f5f6fc6e
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 050ec0b7c3fdc9146a25b1b1f372ee4928d80c09
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den angegebenen Eigenschaftswert der Dateigruppe für bereitgestellte Dateigruppen- und Eigenschaftsnamen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FILEGROUPPROPERTY ( filegroup_name , property )  
```  
  
## <a name="arguments"></a>Argumente  
 *filegroup_name*  
 Ist ein Ausdruck vom Typ **Sysname** , die den Namen der Dateigruppe für die die benannte Eigenschaftsinformation zurückgegeben darstellt.  
  
 *Eigenschaft*  
 Ist ein Ausdruck vom Typ **varchar(128)** enthält den Namen der Eigenschaft "Dateigruppe" zurückgegeben. *Eigenschaft* kann einen der folgenden Werte sein.  
  
|Wert|Description|Rückgabewert|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|Dateigruppe ist schreibgeschützt.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsUserDefinedFG**|Dateigruppe ist eine benutzerdefinierte Dateigruppe.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsDefault**|Dateigruppe ist die Standarddateigruppe.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 *Filegroup_name* entspricht der **Namen** Spalte in der **"Sys.FileGroups"** -Katalogsicht angezeigt.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die Einstellung für die `IsDefault`-Eigenschaft für die primäre Dateigruppe in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
  
SELECT FILEGROUPPROPERTY('PRIMARY', 'IsDefault') AS 'Default Filegroup';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Default Filegroup   
---------------------   
1  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Filegroup_id &#40; Transact-SQL &#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [Filegroup_name &#40; Transact-SQL &#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  

