---
title: Verwenden des Zeichenformats zum Importieren und Exportieren von Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 927bc546612f0d56ce857a41fbb2ba49ca32d47e
ms.contentlocale: de-de
ms.lasthandoff: 10/04/2017

---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>Verwenden des Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)
Das Zeichenformat wird für den Massenexport von Daten in eine Textdatei empfohlen, die in einem anderen Programm verwendet werden sollen, oder für den Massenimport von Daten aus einer Textdatei, die von einem anderen Programm generiert werden.  

Das Zeichenformat verwendet das Zeichendatenformat für alle Spalten. Es ist nützlich, Informationen im Zeichenformat zu speichern, wenn Sie die Daten mit einem anderen Programm, z. B. als Kalkulationstabelle, verwenden, oder die Daten aus einer Datenbank eines anderen Herstellers wie z. B. Oracle in eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kopiert werden müssen.  
  
> [!NOTE]
>  Wenn Sie Daten zwischen Instanzen von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] massenübertragen und die Datendatei Unicode-Zeichendaten, aber keine Sonderzeichen oder DBCS-Zeichen enthält, sollten Sie das Unicode-Zeichenformat verwenden. Weitere Informationen finden Sie unter [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).
  
|In diesem Thema:|
|---|
|[Überlegungen zum Verwenden des Zeichenformats](#considerations)|
|[Befehlsoptionen für das Zeichenformat](#command_options)|
|[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispiel einer Nicht-XML-Formatdatei](#nonxml_format_file)<br />|
|[Beispiele](#examples)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und dem Zeichenformat zum Exportieren von Daten](#bcp_char_export)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und dem Zeichenformat zum Importieren von Daten ohne eine Formatdatei](#bcp_char_import)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und dem Zeichenformat zum Importieren von Daten mit einer Nicht-XML-Formatdatei](#bcp_char_import_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und dem Zeichenformat ohne eine Formatdatei](#bulk_char)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und dem Zeichenformat mit einer Nicht-XML-Formatdatei](#bulk_char_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET und dem Zeichenformat mit einer Nicht-XML-Formatdatei](#openrowset_char_fmt)|
|[Verwandte Aufgaben](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|


  
## Überlegungen zum Verwenden des Zeichenformats<a name="considerations"></a>
Beim Verwenden des Zeichenformats sollten Sie Folgendes berücksichtigen:  
  
-   Das [Hilfsprogramm „bcp“](../../tools/bcp-utility.md) trennt standardmäßig die Zeichendatenfelder mit dem Tabstoppzeichen und schließt die Datensätze mit einem Neue-Zeile-Zeichen ab.  Weitere Informationen zum Angeben alternativer Abschlusszeichen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
-   Standardmäßig werden vor einem Massenexport oder -import von Daten im Zeichenmodus die folgenden Konvertierungen ausgeführt:  
  
    |Richtung des Massenvorgangs|Konvertierung|  
    |---------------------------------|----------------|  
    |Exportieren|Konvertiert Daten in die Zeichendarstellung. Wenn dies explizit angefordert wird, werden die Daten in die angeforderte Codepage für Zeichenspalten konvertiert. Wenn keine Codepage angegeben wird, werden die Zeichendaten mithilfe der OEM-Codepage des Clientcomputers konvertiert.|  
    |Importieren|Konvertiert Zeichendaten bei Bedarf in die systemeigene Darstellung und übersetzt die Zeichendaten von der Codepage des Clients in die Codepage der Zielspalte(n).|  
  
-   Um den Verlust von Sonderzeichen zu verhindern, verwenden Sie das Unicode-Zeichenformat, oder geben Sie eine Codepage an.  
  
-   Alle [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) -Daten, die in einer Zeichenformatdatei gespeichert sind, werden ohne Metadaten gespeichert. Alle Datenwerte werden gemäß den Regeln der impliziten Datenkonvertierung in das [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) -Format konvertiert. Beim Importieren in eine [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) -Spalte werden die Daten als [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)-Datentyp importiert. Beim Importieren in eine Spalte mit einem anderen Datentyp als [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) werden die Daten mithilfe der impliziten Konvertierung von [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) konvertiert. Weitere Informationen zur Datenkonvertierung finden Sie unter [Datentypkonvertierung &#40;Datenbankmodul&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).  
  
-   Das [Hilfsprogramm „bcp“](../../tools/bcp-utility.md) exportiert [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)-Werte in Datendateien im Zeichenformat mit vier Stellen nach dem Dezimaltrennzeichen und ohne Symbole für die Zifferngruppierung, wie z.B. Kommas. So wird z.B. eine [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) -Spalte mit dem Wert 1,234,567.123456 beim Massenkopieren in eine Datendatei als die Zeichenfolge 1234567.1235 massenexportiert.  
  
## Befehlsoptionen für das Zeichenformat<a name="command_options"></a>  
Sie können Daten im Zeichenformat in eine Tabelle importieren, indem Sie die folgenden Anweisungen verwenden: [BCP](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) oder [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Für einen [bcp](../../tools/bcp-utility.md) -Befehl oder eine [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) -Anweisung können Sie das Datenformat in der Anweisung angeben.  Für eine [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)-Anweisung müssen Sie das Datenformat in einer Formatdatei angeben.  
  
Das Zeichenformat wird von den folgenden Befehlsoptionen unterstützt:  
  
|Befehl|Option|Beschreibung|  
|-------------|------------|-----------------|  
|bcp|**-c**|Bewirkt, dass das Hilfsprogramm „bcp“ Zeichendaten verwendet.*|  
|BULK INSERT|DATAFILETYPE **='char'**|Verwendet das Zeichenformat beim Massenimport von Daten.|  
|OPENROWSET|–|Muss eine Formatdatei verwenden|
  
 \*Um Zeichendaten (**-c**) in ein Format zu laden, das mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Clients kompatibel ist, verwenden Sie den Schalter **-V** . Weitere Informationen finden Sie unter [Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
   
> [!NOTE]
>  Alternativ können Sie die Formatierung pro Feld in einer Formatdatei angeben. Weitere Informationen finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).

## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema beschriebenen Beispiele basieren auf einer Tabelle und einer Formatdatei, die nachstehend definiert werden.

### **Beispieltabelle**<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank sowie eine Tabelle namens `myChar` und füllt die Tabelle mit einigen ursprünglichen Werten auf.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myChar ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myChar
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Beispiel einer Nicht-XML-Formatdatei**<a name="nonxml_format_file"></a>
SQL Server unterstützt zwei Typen von Formatdateien: Nicht-XML- und XML-Format.  Nicht-XML ist das ursprüngliche Format, das von früheren Versionen von SQL Server unterstützt wird.  Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myChar.fmt`zu erstellen, die auf dem Schema von `myChar`basiert.  Geben Sie bei der Ausführung eines [bcp](../../tools/bcp-utility.md) -Befehls zum Erstellen einer Formatdatei das **format** -Argument an, und verwenden Sie **nul** anstatt eines Datendateipfads.  Die Option „format“ erfordert außerdem die Option **-f** .  Zusätzlich wird in diesem Beispiel der Qualifizierer **c** verwendet, um Zeichendaten anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
bcp TestDatabase.dbo.myChar format nul -f D:\BCP\myChar.fmt -T -c 

REM Review file
Notepad D:\BCP\myChar.fmt
```

> [!IMPORTANT]
> Stellen Sie sicher, dass Ihre Nicht-XML-Formatdatei mit einem Wagenrücklauf/Zeilenvorschub endet.  Andernfalls wird Ihnen möglicherweise die folgende Fehlermeldung angezeigt:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Beispiele<a name="examples"></a>
In dem folgenden Beispiel werden die Datenbank und die Formatdateien verwendet, die oben erstellt wurden.

### **Verwenden von bcp und dem Zeichenformat zum Exportieren von Daten**<a name="bcp_char_export"></a>
Der Schalter**-c** und der **OUT** -Befehl.  Hinweis: Die in diesem Beispiel erstellte Datendatei wird auch in allen nachfolgenden Beispielen verwendet.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
bcp TestDatabase.dbo.myChar OUT D:\BCP\myChar.bcp -T -c

REM Review results
NOTEPAD D:\BCP\myChar.bcp
```

### **Verwenden von bcp und dem Zeichenformat zum Importieren von Daten ohne eine Formatdatei**<a name="bcp_char_import"></a>
Der Schalter**-c** und der **IN** -Befehl.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -T -c

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **Verwenden von bcp und dem Zeichenformat zum Importieren von Daten mit einer Nicht-XML-Formatdatei**<a name="bcp_char_import_fmt"></a>
Die Schalter**-c** und **-f** switches und **IN** commund.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -f D:\BCP\myChar.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **Verwenden von BULK INSERT und dem Zeichenformat ohne eine Formatdatei**<a name="bulk_char"></a>
**DATAFILETYPE** -Argument.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
    FROM 'D:\BCP\myChar.bcp'
    WITH (
        DATAFILETYPE = 'Char'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Verwenden von BULK INSERT und dem Zeichenformat mit einer Nicht-XML-Formatdatei**<a name="bulk_char_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
   FROM 'D:\BCP\myChar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myChar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Verwenden von OPENROWSET und dem Zeichenformat mit einer Nicht-XML-Formatdatei**<a name="openrowset_char_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar;  -- for testing
INSERT INTO TestDatabase.dbo.myChar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myChar.bcp', 
        FORMATFILE = 'D:\BCP\myChar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```
  
## Verwandte Aufgaben<a name="RelatedTasks"></a>  
So verwenden Sie Datenformate für Massenimport oder Massenexport 
  
-   [Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  

