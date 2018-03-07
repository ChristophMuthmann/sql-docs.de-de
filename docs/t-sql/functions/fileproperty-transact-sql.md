---
title: FILEPROPERTY (Transact-SQL) | Microsoft Docs
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
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce71f17549cb286ed95004c62901337ce39c6739
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Eigenschaftswert für den angegebenen Dateinamen zurück, wenn ein Dateiname in der aktuellen Datenbank und ein Eigenschaftsname angegeben sind. Gibt NULL für Dateien zurück, die nicht in der aktuellen Datenbank sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FILEPROPERTY ( file_name , property )  
```  
  
## <a name="arguments"></a>Argumente  
 *Dateiname*  
 Ein Ausdruck, der den Namen der Datei enthält, die der aktuellen Datenbank zugeordnet ist, für die Eigenschaftsinformationen zurückgegeben werden sollen. *File_name* ist **vom Typ nchar(128)**.  
  
 *Eigenschaft*  
 Ein Ausdruck, der den Namen der zurückzugebenden Dateieigenschaft enthält. *Eigenschaft* ist **varchar(128)**, und kann einen der folgenden Werte.  
  
|Wert|Description|Rückgabewert|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|Dateigruppe ist schreibgeschützt.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsPrimaryFile**|Datei ist die primäre Datei.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**Von IsLogFile**|Datei ist eine Protokolldatei.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**SpaceUsed**|Speicherplatz, der von der angegebenen Datei verwendet wird.|Anzahl der in der Datei zugeordneten Seiten.|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 *File_name* entspricht der **Namen** Spalte in der **Sys. master_files** oder **Sys. database_files** -Katalogsicht angezeigt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Einstellung für die `IsPrimaryFile`-Eigenschaft des `AdventureWorks_Data`-Dateinamens in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
  
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [FILEGROUPPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
