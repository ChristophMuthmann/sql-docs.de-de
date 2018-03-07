---
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
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
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75882e2c74b6a432f49b9b7e14b83af05e961af7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Gibt die Datei-ID für den angegebenen logischen Dateinamen der Daten-, Protokoll- oder Volltextdatei in der aktuellen Datenbank zurück.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>Argumente  
 *Dateiname*  
 Ist ein Ausdruck vom Typ **Sysname** , die den Namen der Datei, für die die Datei-ID zurückgegeben darstellt  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
 **NULL** auf Fehler  
  
## <a name="remarks"></a>Hinweise  
 *File_name* entspricht den logischen Dateinamen angezeigt, der **Namen** Spalte in der [Sys. master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) oder [Sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) Katalogsichten.  
  
 FILE_IDEX kann in einer SELECT-Liste, in einer WHERE-Klausel oder überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. Abrufen der Datei-ID einer angegebenen Datei  
Im folgenden Beispiel wird die Datei-ID für die Datei `AdventureWorks_Data` zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. Abrufen der Datei-ID, wenn der Dateiname nicht bekannt ist  
Das folgende Beispiel gibt die Datei-ID, der die `AdventureWorks` Protokolldatei durch Auswahl aus den logischen Dateinamen der `sys.database_files` -Katalogsicht angezeigt, wobei der Dateityp gleich ist `1` (Protokoll).  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. Abrufen der Datei-ID einer Volltextkatalogdatei  
Das folgende Beispiel gibt die Datei-ID einer Volltext-Datei durch Auswahl aus den logischen Dateinamen der `sys.database_files` -Katalogsicht angezeigt, wobei der Dateityp gleich ist `4` (Volltextsuche). Dieses Beispiel gibt NULL zurück, wenn ein Volltextkatalog nicht vorhanden ist.  
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
