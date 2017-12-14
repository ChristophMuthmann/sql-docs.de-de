---
title: Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5fd105a2da0e4822ee3da0b2f8929f70d0185cb5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Es wird empfohlen, für die Massenübertragung von Daten zwischen mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe einer Datendatei, die Sonderzeichen oder Zeichen aus dem Doppelbyte-Zeichensatz (Double-Byte Character Set, DBCS) enthält, das Unicode-Zeichenformat zu verwenden. Mit dem Unicode-Zeichenformat können Daten von einem Server mithilfe einer Codepage exportiert werden, wenn sich diese Codepage von der Codepage unterscheidet, die der Client verwendet, der den Vorgang ausführt. In solchen Fällen bietet die Verwendung des Unicode-Zeichenformats folgende Vorteile:  
  
* Wenn es sich bei den Quell- und Zieldaten um Unicode-Datentypen handelt, bleiben bei Verwendung des Unicode-Zeichenformats alle Zeichendaten erhalten.  
  
* Wenn es sich bei den Quell- und Zieldaten nicht um Unicode-Datentypen handelt, wird durch die Verwendung des Unicode-Datenformats der Verlust von Sonderzeichen in Bezug auf die Quelldaten minimiert, die am Ziel nicht dargestellt werden können.

|In diesem Thema:|
|---|
|[Überlegungen zur Verwendung des Unicode-Zeichenformats](#considerations)|
|[Besondere Überlegungen zur Verwendung des Unicode-Zeichenformats, bcp und einer Formatdatei](#special_considerations)|
|[Befehlsoptionen für das Unicode-Zeichenformat](#command_options)|
|[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispiel einer Nicht-XML-Formatdatei](#nonxml_format_file)|
|[Beispiele](#examples)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und dem Unicode-Zeichenformat zum Exportieren von Daten](#bcp_widechar_export)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und dem Unicode-Zeichenformat zum Importieren von Daten ohne eine Formatdatei](#bcp_widechar_import)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und dem Unicode-Zeichenformat zum Importieren von Daten mit einer Nicht-XML-Formatdatei](#bcp_widechar_import_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und dem Unicode-Zeichenformat ohne eine Formatdatei](#bulk_widechar)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und dem Unicode-Zeichenformat mit einer Nicht-XML-Formatdatei](#bulk_widechar_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET und dem Unicode-Zeichenformat mit einer Nicht-XML-Formatdatei](#openrowset_widechar_fmt)|
|[Verwandte Aufgaben](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
 
## Überlegungen zur Verwendung des Unicode-Zeichenformats<a name="considerations"></a>
Beim Verwenden des Unicode-Zeichenformats sollten Sie Folgendes berücksichtigen:  

* Das [Hilfsprogramm „bcp“](../../tools/bcp-utility.md) trennt standardmäßig die Zeichendatenfelder mit dem Tabstoppzeichen und schließt die Datensätze mit einem Neue-Zeile-Zeichen ab.  Weitere Informationen zum Angeben alternativer Abschlusszeichen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).

* Die [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)-Daten, die in einer Datendatei im Unicode-Zeichenformat gespeichert sind, verhalten sich wie Daten in einer Datendatei im Zeichenformat, außer dass die Daten als [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)-Daten und nicht als [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)-Daten gespeichert sind. Weitere Informationen zum Zeichenformat finden Sie unter [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md).  

## Besondere Überlegungen zur Verwendung des Unicode-Zeichenformats, bcp und einer Formatdatei<a name="special_considerations"></a>
Datendateien im Unicode-Zeichenformat folgen den Konventionen für Unicode-Dateien.  Die ersten zwei Bytes der Datei sind Hexadezimalzahlen (0xFFFE).  Diese Bytes dienen als Markierungen für die Bytereihenfolge (byte-order marks; BOM), in der angegeben wird, ob das höherwertige Byte in der Datei zuerst oder zuletzt gespeichert wird.  Das [Hilfsprogramm „bcp“](../../tools/bcp-utility.md) kann die BOM falsch interpretieren, was dazu führt, dass der Importvorgang teilweise fehlschlägt. Sie erhalten dann möglicherweise eine ähnliche Fehlermeldung wie die folgende:
```
Starting copy...
SQLState = 22005, NativeError = 0
Error = [Microsoft][ODBC Driver 13 for SQL Server]Invalid character value for cast specification
```

Die BOM kann unter den folgenden Umständen falsch interpretiert werden:
* Um Unicode-Zeichen anzugeben, werden das [Hilfsprogramm „bcp“](../../tools/bcp-utility.md) und der Schalter **-w** verwendet.

* Es wird eine Formatdatei verwendet.

* Das erste Feld in der Datendatei enthält ein Nichtzeichen.

Ziehen Sie in Erwägung, ob eine der folgenden Problemumgehungen für Ihre *besondere* Situation möglicherweise in Betracht kommt:
* Verwenden Sie keine Formatdatei.  Ein Beispiel dieser Lösung finden Sie in diesem Artikel unter [Verwenden von BCP und dem Unicode-Zeichenformat zum Importieren von Daten ohne eine Formatdatei](#bcp_widechar_import).

* Verwenden den Schalter **-c** anstelle von **-w**.

* Exportieren Sie die Daten mit einem nativen Format erneut.

* Verwenden Sie [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  Beispiele für diese Problemumgehungen finden Sie nachfolgend unter [Verwenden von BULK INSERT und dem Unicode-Zeichenformat mit einer Nicht-XML-Formatdatei](#bulk_widechar_fmt) und [Verwenden von OPENROWSET und dem Unicode-Zeichenformat mit einer Nicht-XML-Formatdatei](#openrowset_widechar_fmt).
 
* Fügen Sie manuell den ersten Datensatz in die Zieltabelle ein, und verwenden Sie anschließend den Schalter **-F 2** , um den Importvorgang für den zweiten Datensatz zu starten.

* Fügen Sie manuell den ersten Dummy-Datensatz in die Datendatei ein, und verwenden Sie anschließend den Schalter **-F 2** , um den Importvorgang für den zweiten Datensatz zu starten.  Ein Beispiel dieser Problemumgehung finden Sie in diesem Artikel unter [Verwenden von BCP und dem Unicode-Zeichenformat zum Importieren von Daten mit einer Nicht-XML-Formatdatei](#bcp_widechar_import_fmt).

* Verwenden Sie eine Stagingtabelle, in der die erste Spalte einen Zeichendatentyp enthält.

* Exportieren Sie die Daten erneut, und ändern Sie die Reihenfolge der Felder, sodass das erste Datenfeld ein Zeichen enthält.  Verwenden Sie anschließend eine Formatdatei, um das Datenfeld der tatsächliche Reihenfolge in der Tabelle neu zuzuordnen.  Ein Beispiel finden Sie unter [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md).
  
## Befehlsoptionen für das Unicode-Zeichenformat<a name="command_options"></a>  
Sie können Daten im Unicode-Zeichenformat in eine Tabelle importieren, indem Sie [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Für einen [bcp](../../tools/bcp-utility.md) -Befehl oder eine [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) -Anweisung können Sie das Datenformat in der Anweisung angeben.  Für eine [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)-Anweisung müssen Sie das Datenformat in einer Formatdatei angeben.  
  
Das Unicode-Zeichenformat wird von den folgenden Befehlsoptionen unterstützt:  
  
|Befehl|Option|Beschreibung|  
|-------------|------------|-----------------|  
|bcp|**-w**|Verwendet das Unicode-Zeichenformat|  
|BULK INSERT|DATAFILETYPE **='widechar'**|Verwendet das Unicode-Zeichenformat beim Massenimport von Daten|  
|OPENROWSET|–|Muss eine Formatdatei verwenden|
  
> [!NOTE]
>  Alternativ können Sie die Formatierung pro Feld in einer Formatdatei angeben. Weitere Informationen finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  
## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema beschriebenen Beispiele basieren auf einer Tabelle und einer Formatdatei, die nachstehend definiert werden.

### **Beispieltabelle**<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank sowie eine Tabelle namens `myWidechar` und füllt die Tabelle mit einigen ursprünglichen Werten auf.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidechar ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidechar
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidechar;
```

### **Beispiel einer Nicht-XML-Formatdatei**<a name="nonxml_format_file"></a>
SQL Server unterstützt zwei Typen von Formatdateien: Nicht-XML- und XML-Format.  Nicht-XML ist das ursprüngliche Format, das von früheren Versionen von SQL Server unterstützt wird.  Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myWidechar.fmt`zu erstellen, die auf dem Schema von `myWidechar`basiert.  Geben Sie bei der Ausführung eines [bcp](../../tools/bcp-utility.md) -Befehls zum Erstellen einer Formatdatei das **format** -Argument an, und verwenden Sie **nul** anstatt eines Datendateipfads.  Die Option „format“ erfordert außerdem die Option **-f** .  Zusätzlich wird in diesem Beispiel der Qualifizierer **c** verwendet, um Zeichendaten anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:

```
bcp TestDatabase.dbo.myWidechar format nul -f D:\BCP\myWidechar.fmt -T -w

REM Review file
Notepad D:\BCP\myWidechar.fmt
```

> [!IMPORTANT]
> Stellen Sie sicher, dass Ihre Nicht-XML-Formatdatei mit einem Wagenrücklauf/Zeilenvorschub endet.  Andernfalls wird Ihnen möglicherweise die folgende Fehlermeldung angezeigt:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`


## Beispiele<a name="examples"></a>
In dem folgenden Beispiel werden die Datenbank und die Formatdateien verwendet, die oben erstellt wurden.

### **Verwenden von bcp und dem Unicode-Zeichenformat zum Exportieren von Daten**<a name="bcp_widechar_export"></a>
Der Schalter**-w** und der **OUT** -Befehl.  Hinweis: Die in diesem Beispiel erstellte Datendatei wird auch in allen nachfolgenden Beispielen verwendet.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w

REM Review results
NOTEPAD D:\BCP\myWidechar.bcp
```

### **Verwenden von bcp und dem Unicode-Zeichenformat zum Importieren von Daten ohne eine Formatdatei**<a name="bcp_widechar_import"></a>
Der Schalter**-w** und der **IN** -Befehl.  Geben Sie folgende Befehle an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Import data
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -T -w

REM Review results is SSMS
```

### **Verwenden von bcp und dem Unicode-Zeichenformat zum Importieren von Daten mit einer Nicht-XML-Formatdatei**<a name="bcp_widechar_import_fmt"></a>
Die Schalter**-w** und **-f** switches und **IN** commund.  Da in diesem Beispiel bcp, eine Formatdatei und Unicode-Zeichen verwendet werden und das erste Datenfeld in der Datendatei ein Nichtzeichen enthält, muss eine Problemumgehung angewendet werden.  Weitere Informationen finden Sie weiter oben in diesem Artikel unter [Besondere Überlegungen zur Verwendung des Unicode-Zeichenformats, bcp und einer Formatdatei](#special_considerations).  Die Datendatei `myWidechar.bcp` wird durch Hinzufügen eines zusätzlichen Datensatzes als „Dummy“-Datensatz geändert, der dann mit dem Schalter `-F 2` ausgelassen wird.

Geben Sie an der Befehlszeile die folgenden Befehle ein, und führen Sie die folgenden Änderungsschritte aus:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Open data file
Notepad D:\BCP\myWidechar.bcp
REM Copy first record and then paste as new first record.  This additional record is the "dummy" record.
REM Close file.

REM Import data instructing bcp to skip dummy record with the -F 2 switch.
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -f D:\BCP\myWidechar.fmt -T -F 2

REM Review results is SSMS

REM Return data file to original state for usage in other examples
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w
```
  
### **Verwenden von BULK INSERT und dem Unicode-Zeichenformat ohne eine Formatdatei**<a name="bulk_widechar"></a>
**DATAFILETYPE** -Argument.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
    FROM 'D:\BCP\myWidechar.bcp'
    WITH (
        DATAFILETYPE = 'widechar'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **Verwenden von BULK INSERT und dem Unicode-Zeichenformat mit einer Nicht-XML-Formatdatei**<a name="bulk_widechar_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
   FROM 'D:\BCP\myWidechar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidechar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **Verwenden von OPENROWSET und dem Unicode-Zeichenformat mit einer Nicht-XML-Formatdatei**<a name="openrowset_widechar_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar;  -- for testing
INSERT INTO TestDatabase.dbo.myWidechar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidechar.bcp', 
        FORMATFILE = 'D:\BCP\myWidechar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
 
  
## Verwandte Aufgaben<a name="RelatedTasks"></a>
So verwenden Sie Datenformate für Massenimport oder Massenexport  
-   [Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
