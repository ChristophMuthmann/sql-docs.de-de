---
title: Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0d6a9d104b6dccc05ca4f4a9c97118d252966a8d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>Verwenden des systemeigenen Unicode-Formats zum Importieren oder Exportieren von Daten (SQL Server)
Das native Unicode-Format ist hilfreich, wenn Informationen von einer Installation von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere kopiert werden müssen. Durch die Verwendung des systemeigenen Formats bei nicht auf Zeichen basierenden Daten kann Zeit eingespart werden, da die unnötige Konvertierung der Datentypen in und aus dem Zeichenformat entfällt. Die Verwendung des Unicode-Zeichenformats für alle Zeichendaten verhindert, dass es zum Verlust von erweiterten Zeichen beim Massenübertragen von Daten zwischen Servern mit unterschiedlichen Codepages kommt. Eine Datendatei im systemeigenen Unicode-Format kann von jeder Massenimportmethode gelesen werden.  
  
 Das systemeigene Unicode-Format wird für die Massenübertragung von Daten zwischen mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe einer Datendatei, die Sonderzeichen oder DBCS-Zeichen enthält, empfohlen. Für nicht auf Zeichen basierende Daten verwendet das systemeigene Unicode-Format systemeigene (Datenbank-)Datentypen. Bei Zeichendaten wie [char](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)und [ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)verwendet das native Unicode-Format das Unicode-Zeichendatenformat.  
  
 Die [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) -Daten, die in einer Datendatei im nativen Unicode-Format als SQLVARIANT gespeichert werden, funktionieren auf die gleiche Weise wie in einer Datendatei im nativen Format, mit der Ausnahme, dass Werte der Typen [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) und [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) in [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) und [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)konvertiert werden. Hierdurch verdoppelt sich der für die entsprechenden Spalten benötigte Speicherplatz. Die ursprünglichen Metadaten bleiben erhalten, und die Werte werden zurück in die ursprünglichen Datentypen [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) und [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) konvertiert, wenn sie in eine Tabellenspalte massenimportiert werden.  
 
 |In diesem Thema:|
|---|
|[Befehlsoptionen für das systemeigene Unicode-Format](#command_options)|
|[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispiel einer Nicht-XML-Formatdatei](#nonxml_format_file)|
|[Beispiele](#examples)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und des nativen Unicode-Zeichenformats zum Exportieren von Daten](#bcp_widenative_export)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und des nativen Unicode-Zeichenformats zum Importieren von Daten ohne eine Formatdatei](#bcp_widenative_import)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und des nativen Unicode-Zeichenformats zum Importieren von Daten mit einer Nicht-XML-Formatdatei](#bcp_widenative_import_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und des nativen Unicode-Zeichenformats ohne eine Formatdatei](#bulk_widenative)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und des nativen Unicode-Zeichenformats mit einer Nicht-XML-Formatdatei](#bulk_widenative_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET und des nativen Unicode-Zeichenformats mit einer Nicht-XML-Formatdatei](#openrowset_widenative_fmt)|
|[Verwandte Aufgaben](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
  
## Befehlsoptionen für das systemeigene Unicode-Format<a name="command_options"></a>  
Sie können Daten im nativen Unicode-Format in eine Tabelle importieren, indem Sie folgende Anweisungen verwenden: [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Für einen [bcp](../../tools/bcp-utility.md) -Befehl oder eine [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) -Anweisung können Sie das Datenformat in der Anweisung angeben.  Für eine [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)-Anweisung müssen Sie das Datenformat in einer Formatdatei angeben.  
  
Das native Unicode-Format wird durch die folgenden Befehlsoptionen unterstützt:  
  
|Befehl|Option|Beschreibung|  
|-------------|------------|-----------------|  
|bcp|**-N**|Bewirkt, dass das Hilfsprogramm **bcp** das native Unicode-Format verwendet, welches das native (Datenbank-)Datentypen für alle nicht auf Zeichen basierenden Daten und das Unicode-Zeichendatenformat für alle Zeichendaten (**char**, **nchar**, **varchar**, **nvarchar**, **text**und **ntext**) verwendet.|  
|BULK INSERT|DATAFILETYPE **='widenative'**|Verwendet das native Unicode-Format beim Massenimportieren von Daten|  
|OPENROWSET|–|Muss eine Formatdatei verwenden|
    
> [!NOTE]
>  Alternativ können Sie die Formatierung pro Feld in einer Formatdatei angeben. Weitere Informationen finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  
## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema beschriebenen Beispiele basieren auf einer Tabelle und einer Formatdatei, die nachstehend definiert werden.

### **Beispieltabelle**<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank sowie eine Tabelle namens `myWidenative` und füllt die Tabelle mit einigen ursprünglichen Werten auf.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidenative ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidenative
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **Beispiel einer Nicht-XML-Formatdatei**<a name="nonxml_format_file"></a>
SQL Server unterstützt zwei Typen von Formatdateien: Nicht-XML- und XML-Format.  Nicht-XML ist das ursprüngliche Format, das von früheren Versionen von SQL Server unterstützt wird.  Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myWidenative.fmt`zu erstellen, die auf dem Schema von `myWidenative`basiert.  Geben Sie bei der Ausführung eines [bcp](../../tools/bcp-utility.md) -Befehls zum Erstellen einer Formatdatei das **format** -Argument an, und verwenden Sie **nul** anstatt eines Datendateipfads.  Die Option „format“ erfordert außerdem die Option **-f** .  Zusätzlich wird in diesem Beispiel der Qualifizierer **c** verwendet, um Zeichendaten anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:

```
bcp TestDatabase.dbo.myWidenative format nul -f D:\BCP\myWidenative.fmt -T -N

REM Review file
Notepad D:\BCP\myWidenative.fmt
```

> [!IMPORTANT]
> Stellen Sie sicher, dass Ihre Nicht-XML-Formatdatei mit einem Wagenrücklauf/Zeilenvorschub endet.  Andernfalls wird Ihnen möglicherweise die folgende Fehlermeldung angezeigt:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Beispiele<a name="examples"></a>
In dem folgenden Beispiel werden die Datenbank und die Formatdateien verwendet, die oben erstellt wurden.

### **Verwenden von bcp und des nativen Unicode-Zeichenformats zum Exportieren von Daten**<a name="bcp_widenative_export"></a>
Der Schalter**-N** und der **OUT** -Befehl.  Hinweis: Die in diesem Beispiel erstellte Datendatei wird auch in allen nachfolgenden Beispielen verwendet.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myWidenative OUT D:\BCP\myWidenative.bcp -T -N

REM Review results
NOTEPAD D:\BCP\myWidenative.bcp
```

### **Verwenden von bcp und des nativen Unicode-Zeichenformats zum Importieren von Daten ohne eine Formatdatei**<a name="bcp_widenative_import"></a>
Der Schalter**-N** und der **IN** -Befehl.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidenative;"

REM Import data
bcp TestDatabase.dbo.myWidenative IN D:\BCP\myWidenative.bcp -T -N

REM Review results is SSMS
```

### **Verwenden von bcp und des nativen Unicode-Zeichenformats zum Importieren von Daten mit einer Nicht-XML-Formatdatei**<a name="bcp_widenative_import_fmt"></a>
Die Schalter**-N** und **-f** switches und **IN** commund.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidenative;"

REM Import data
bcp TestDatabase.dbo.myWidenative IN D:\BCP\myWidenative.bcp -f D:\BCP\myWidenative.fmt -T

REM Review results is SSMS
```

### **Verwenden von BULK INSERT und des nativen Unicode-Zeichenformats ohne eine Formatdatei**<a name="bulk_widenative"></a>
**DATAFILETYPE** -Argument.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative; -- for testing
BULK INSERT TestDatabase.dbo.myWidenative
    FROM 'D:\BCP\myWidenative.bcp'
    WITH (
        DATAFILETYPE = 'widenative'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **Verwenden von BULK INSERT und des nativen Unicode-Zeichenformats mit einer Nicht-XML-Formatdatei**<a name="bulk_widenative_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative; -- for testing
BULK INSERT TestDatabase.dbo.myWidenative
   FROM 'D:\BCP\myWidenative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidenative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **Verwenden von OPENROWSET und des nativen Unicode-Zeichenformats mit einer Nicht-XML-Formatdatei**<a name="openrowset_widenative_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative;  -- for testing
INSERT INTO TestDatabase.dbo.myWidenative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidenative.bcp', 
        FORMATFILE = 'D:\BCP\myWidenative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

## Verwandte Aufgaben<a name="RelatedTasks"></a>
So verwenden Sie Datenformate für Massenimport oder Massenexport  
-   [Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
