---
title: FileTableRootPath (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs: TSQL
helpviewer_keywords: FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 475c76c68198719de312a6a7ca9485097596d624
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt den UNC-Pfad auf der Stammebene für eine bestimmte FileTable oder die aktuelle Datenbank zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FileTableRootPath ( [ ‘[schema_name.]FileTable_name’ ], @option )  
```  
  
## <a name="arguments"></a>Argumente  
 *FileTable_name*  
 Der Name der FileTable. *FileTable_name* ist vom Typ **Nvarchar**. Dies ist ein optionaler Parameter. Der Standardwert ist die aktuelle Datenbank. Angeben von *Schema_name* ist ebenfalls optional. Sie können NULL übergeben, für *FileTable_name* Standardparameterwert zu verwenden  
  
 *@option*  
 Ein ganzzahliger Ausdruck, der definiert, wie die Serverkomponente des Pfads formatiert werden soll. *@option*Dabei kann es sich um einen der folgenden Werte aufweisen:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Gibt den in ein NetBIOS-Format konvertierten Servernamen zurück. Beispiel:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDB`<br /><br /> Dies ist der Standardwert.|  
|**1**|Gibt den Servernamen ohne Konvertierung zurück. Beispiel:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDB`|  
|**2**|Gibt den vollständigen Serverpfad zurück. Beispiel:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDB`|  
  
## <a name="return-type"></a>Rückgabetyp  
 **nvarchar(4000)**  
  
 Wenn die Datenbank zu einer Always On-verfügbarkeitsgruppe gehört die **FileTableRootPath** Funktion gibt den virtuellen Netzwerknamen (VNN) statt des Computernamens zurück.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die **FileTableRootPath** Funktion gibt NULL zurück, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Der Wert der *FileTable_name* ist ungültig.  
  
-   Der Aufrufer hat keine ausreichende Berechtigung zum Verweisen auf die angegebene Tabelle oder die aktuelle Datenbank auf.  
  
-   Die FILESTREAM-Option von *Database_directory* ist nicht für die aktuelle Datenbank festgelegt.  
  
 Weitere Informationen finden Sie unter [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Um Code und Anwendungen vom aktuellen Computer und von der Datenbank unabhängig zu halten, sollten Sie keinen Code schreiben, der auf absoluten Dateipfaden basiert. Rufen Sie stattdessen den vollständigen Pfad für eine Datei mit der Funktion **FileTableRootPath** und der Funktion **GetFileNamespacePath** zur Laufzeit ab, wie im folgenden Beispiel gezeigt. Die **GetFileNamespacePath** -Funktion gibt standardmäßig den relativen Pfad der Datei unter dem Stammpfad der Datenbank zurück.  
  
```tsql  
USE MyDocumentDB;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Die **FileTableRootPath** -Funktion erfordert:  
  
-   SELECT-Berechtigung für die FileTable, um den Stammpfad einer bestimmten FileTable abzurufen.  
  
-   **"db_datareader"** oder höhere Berechtigung, um den Stammpfad für die aktuelle Datenbank abzurufen.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele zeigen, wie zum Aufrufen der **FileTableRootPath** Funktion.  
  
```  
USE MyDocumentDB;  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB”  
SELECT FileTableRootPath();  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
