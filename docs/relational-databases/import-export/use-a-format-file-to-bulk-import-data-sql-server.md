---
title: Massenimport von Daten mithilfe einer Formatdatei (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: bbcc9359fafd0a0498eba7fea31367ca36438125
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Massenimport von Daten mithilfe einer Formatdatei (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

In diesem Thema wird die Verwendung einer Formatdatei bei Massenimportvorgängen beschrieben.  Eine Formatdatei ordnet die Felder der Datendatei den Spalten einer Tabelle zu.  Weitere Informationen finden Sie unter [Erstellen einer Formatdatei (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) .

|Outline|
|---|
|[Vorbereitungen](#begin)<br />[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispieldatendatei](#sample_data_file)<br />[Erstellen der Formatdateien](#create_format_file)<br />&emsp;&#9679;&emsp;[Erstellen einer Nicht-XML-Formatdatei](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Erstellen einer XML-Formatdatei](#xml_format_file)<br />[Verwenden einer Formatdatei für einen Massenimport von Daten](#import_data)<br />&emsp;&#9679;&emsp;[Verwenden von BCP- und der Nicht-XML-Formatdatei](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und der XML-Formatdatei](#bcp_xml)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und der Nicht-XML-Formatdatei](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und der XML-Formatdatei](#bulk_xml)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und der Nicht-XML-Formatdatei](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und der XML-Formatdatei](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
## Vorbereitungen<a name="begin"></a>
* Damit eine Formatdatei mit einer Datendatei mit Unicode-Zeichen verwendet werden kann, müssen alle Eingabefelder Unicode-Textzeichenfolgen enthalten (d.h., entweder Unicode-Zeichenfolgen einer festen Länge oder Unicode-Zeichenfolgen mit Abschlusszeichen).
* Verwenden Sie in der Formatdatei einen der folgenden Datentypen für den Massenexport oder -import von [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) -Daten:
  * SQLCHAR or SQLVARYCHAR (die Daten werden in der Clientcodepage gesendet bzw. in der durch die Sortierung implizierten Codeseite)
  * SQLNCHAR oder SQLNVARCHAR (die Daten werden als Unicode gesendet)
  * SQLBINARY or SQLVARYBIN (die Daten werden ohne Konvertierung gesendet)
* Azure SQL-Datenbank und Azure SQL Data Warehouse unterstützen nur das Hilfsprogramm [bcp](../../tools/bcp-utility.md).  Weitere Informationen finden Sie unter:
  * [Laden von Daten in Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-load/)
  * [Laden von Daten aus SQL Server in Azure SQL Data Warehouse (Flatfiles)](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-from-sql-server-with-bcp/)
  * [Migrieren von Daten](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-migrate-data/)

## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema enthaltenen Beispiele für Formatdateien basieren auf der Tabelle und der Datendatei, die nachstehend definiert sind.

### **Beispieltabelle**<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank und eine Tabelle namens `myFirstImport`.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.MyFirstImport (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   BirthDate Date
   );
```

### **Beispieldatendatei**<a name="sample_data_file"></a>
Erstellen Sie mit Editor die leere Datei `D:\BCP\myFirstImport.bcp` , und fügen Sie die folgenden Daten ein:
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

Alternativ können Sie das folgende PowerShell-Skript ausführen, um die Datei zu erstellen und aufzufüllen:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = Join-Path -Path $dir -ChildPath 'MyFirstImport.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

## Erstellen der Formatdateien<a name="create_format_file"></a>
SQL Server unterstützt zwei Typen von Formatdateien: Nicht-XML- und XML-Format.  Nicht-XML ist das ursprüngliche Format, das von früheren Versionen von SQL Server unterstützt wird.

### **Erstellen einer Nicht-XML-Formatdatei**<a name="nonxml_format_file"></a>
Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myFirstImport.fmt`zu erstellen, die auf dem Schema von `myFirstImport`basiert.  Geben Sie das **format** -Argument an, um einen bcp-Befehl zum Erstellen einer Formatdatei zu verwenden, und verwenden Sie **nul** anstatt eines Datendateipfads.  Die Option „format“ erfordert außerdem die Option **-f** .  Zusätzlich werden folgende Qualifizierer verwendet: **c** , um Zeichendaten anzugeben, **t** , um ein Komma als [Feldabschlusszeichen](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -f D:\BCP\myFirstImport.fmt -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.fmt
```

Ihre Nicht-XML-Formatdatei `D:\BCP\myFirstImport.fmt` sollte wie folgt aussehen:
```
13.0
4
1       SQLCHAR             0       7       ","      1     PersonID               ""
2       SQLCHAR             0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR             0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR             0       11      "\r\n"   4     BirthDate              ""
```

> [!IMPORTANT]
> Stellen Sie sicher, dass Ihre Nicht-XML-Formatdatei mit einem Wagenrücklauf/Zeilenvorschub endet.  Andernfalls wird Ihnen möglicherweise die folgende Fehlermeldung angezeigt:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

### **Erstellen einer XML-Formatdatei**<a name="xml_format_file"></a>  
Ausführliche Informationen finden Sie unter [XML-Formatdateien (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die XML-Formatdatei `myFirstImport.xml`zu erstellen, die auf dem Schema von `myFirstImport`basiert. Geben Sie das **format** -Argument an, um einen bcp-Befehl zum Erstellen einer Formatdatei zu verwenden, und verwenden Sie **nul** anstatt eines Datendateipfads.  Für die Formatoption ist immer auch die Option **-f** erforderlich. Zum Erstellen einer XML-Formatdatei muss zudem die Option **-x** angegeben werden.  Zusätzlich werden folgende Qualifizierer verwendet: **c** , um Zeichendaten anzugeben, **t** , um ein Komma als [Feldabschlusszeichen](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

Ihre XML-Formatdatei `D:\BCP\myFirstImport.xml` sollte wie folgt aussehen:
```xml
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## Verwenden einer Formatdatei für einen Massenimport von Daten<a name="import_data"></a>
In den folgenden Beispielen werden die Datenbank, die Datendatei und die Formatdateien verwendet, die oben erstellt wurden.

### **Verwenden von [bcp](../../tools/bcp-utility.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_nonxml"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### **Verwenden von [bcp](../../tools/bcp-utility.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bcp_xml"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_nonxml"></a>
Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bulk_xml"></a>
Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_nonxml"></a>    
Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="openrowset_xml"></a>
Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```
  
## <a name="more-examples"></a>Weitere Beispiele  
 [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Nicht-XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [Formatdateien zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
  
