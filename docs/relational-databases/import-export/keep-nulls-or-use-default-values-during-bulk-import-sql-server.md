---
title: "Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 12b379c1d02dc07a5581a5a3f3585f05f763dad7
ms.openlocfilehash: 74e0dabe8b6691e467e82d7267c40ef578d84490
ms.contentlocale: de-de
ms.lasthandoff: 10/04/2017

---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Wenn Daten in eine Tabelle importiert werden, werden standardmäßig alle für die Spalten in der Tabelle definierten Standardwerte durch den Befehl [bcp](../../tools/bcp-utility.md) und die Anweisung [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) überwacht.  Wenn beispielsweise ein NULL-Feld in einem Datenfeld vorkommt, wird stattdessen der Standardwert für die Spalte geladen.  Sowohl mit dem Befehl [bcp](../../tools/bcp-utility.md) als auch mit der Anweisung [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) können Sie angeben, dass NULL-Werte beibehalten werden sollen.

Eine reguläre INSERT-Anweisung hingegen behält den NULL-Wert bei, statt einen Standardwert einzufügen. Die INSERT ... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)-Anweisung zeigt dasselbe grundlegende Verhalten wie eine reguläre INSERT-Anweisung, unterstützt jedoch zusätzlich einen [Tabellenhinweis](../../t-sql/queries/hints-transact-sql-table.md) zum Einfügen der Standardwerte.

|Outline|
|---|
|[Beibehalten von NULL-Werten](#keep_nulls)<br />[Verwenden von Standardwerten mit INSERT ... SELECT * FROM OPENROWSET(BULK...)](#keep_default)<br />[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispieldatendatei](#sample_data_file)<br />&emsp;&#9679;&emsp;[Beispiel einer Nicht-XML-Formatdatei](#nonxml_format_file)<br />[Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports](#import_data)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und Beibehalten von NULL-Werten ohne Formatdatei](#bcp_null)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und Beibehalten von NULL-Werten mit einer Nicht-XML-Formatdatei](#bcp_null_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und Verwenden von Standardwerten ohne Formatdatei](#bcp_default)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und Verwenden von Standardwerten mit einer Nicht-XML-Formatdatei](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und Beibehalten von NULL-Werten ohne Formatdatei](#bulk_null)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und Beibehalten von NULL-Werten mit einer Nicht-XML-Formatdatei](#bulk_null_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und Verwenden von Standardwerten ohne Formatdatei](#bulk_default)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und Verwenden von Standardwerten mit einer Nicht-XML-Formatdatei](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und Beibehalten von NULL-Werten mit einer Nicht-XML-Formatdatei](#openrowset__null_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und Verwenden von Standardwerten mit einer Nicht-XML-Formatdatei](#openrowset__default_fmt)

## Beibehalten von NULL-Werten<a name="keep_nulls"></a>  
Die folgenden Qualifizierer geben an, dass ein leeres Feld in der Datendatei seinen NULL-Wert während des Massenimportvorgangs beibehält, statt (ggf.) einen Standardwert für die Tabellenspalten zu übernehmen.  Standardmäßig werden für [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md), Spalten, die nicht im Massenladevorgang angegeben sind, auf NULL festgelegt.
  
|Befehl|Qualifizierer|Qualifizierertyp|  
|-------------|---------------|--------------------|  
|bcp|-k|Schalter|  
|BULK INSERT|KEEPNULLS**\***|Argument|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|–|–|  
  
**\*** Für [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)muss, wenn keine Standardwerte verfügbar sind, die Tabellenspalte für das Zulassen von NULL-Werten definiert sein. 
  
> [!NOTE]
> Diese Qualifizierer deaktivieren das Prüfen von DEFAULT-Definitionen in einer Tabelle durch diese Massenimportbefehle.  Für gleichzeitige INSERT-Anweisungen werden jedoch DEFAULT-Definitionen erwartet.
 
## Verwenden von Standardwerten mit INSERT ... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)<a name="keep_default"></a>  
Sie können angeben, dass die entsprechende Tabellenspalte für ein leeres Feld in der Datendatei den Standardwert verwendet (falls vorhanden).  Verwenden Sie den Tabellenhinweis [KEEPDEFAULTS](../../t-sql/queries/hints-transact-sql-table.md), um Standardwerte zu verwenden.
 
> [!NOTE]
>  Weitere Informationen finden Sie unter [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) und [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)

## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema beschriebenen Beispiele basieren auf einer Tabelle, einer Datendatei und einer Formatdatei, die nachstehend definiert werden.

### **Beispieltabelle**<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank und eine Tabelle namens `myNulls`.  Beachten Sie, dass die vierte Tabellenspalte `Kids`einen Standardwert hat.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNulls ( 
   PersonID smallint not null,
   FirstName varchar(25),
   LastName varchar(30),
   Kids varchar(13) DEFAULT 'Default Value',
   BirthDate date
   );
```

### **Beispieldatendatei**<a name="sample_data_file"></a>
Erstellen Sie im Editor die leere Datei `D:\BCP\myNulls.bcp` , und fügen Sie die nachstehenden Daten ein.  Beachten Sie, dass im dritten Datensatz in der vierten Spalte kein Wert vorhanden ist.

```
1,Anthony,Grosse,Yes,1980-02-23
2,Alica,Fatnowna,No,1963-11-14
3,Stella,Rosenhain,,1992-03-02
```

Alternativ können Sie das folgende PowerShell-Skript ausführen, um die Datei zu erstellen und aufzufüllen:

```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'MyNulls.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,Yes,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,No,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```
  
### **Beispiel einer Nicht-XML-Formatdatei**<a name="nonxml_format_file"></a>
SQL Server unterstützt zwei Typen von Formatdateien: Nicht-XML- und XML-Format.  Nicht-XML ist das ursprüngliche Format, das von früheren Versionen von SQL Server unterstützt wird.  Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myNulls.fmt`zu erstellen, die auf dem Schema von `myNulls`basiert.  Geben Sie bei der Ausführung eines [bcp](../../tools/bcp-utility.md) -Befehls zum Erstellen einer Formatdatei das **format** -Argument an, und verwenden Sie **nul** anstatt eines Datendateipfads.  Die Option „format“ erfordert außerdem die Option **-f** .  Zusätzlich werden folgende Qualifizierer verwendet: **c** , um Zeichendaten anzugeben, **t** , um ein Komma als [Feldabschlusszeichen](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
bcp TestDatabase.dbo.myNulls format nul -c -f D:\BCP\myNulls.fmt -t, -T

REM Review file
Notepad D:\BCP\myNulls.fmt
```

> [!IMPORTANT]
> Stellen Sie sicher, dass Ihre Nicht-XML-Formatdatei mit einem Wagenrücklauf/Zeilenvorschub endet.  Andernfalls wird Ihnen möglicherweise die folgende Fehlermeldung angezeigt:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

 Weitere Informationen zum Erstellen von Formatdateien finden Sie unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md), um Standardwerte zu verwenden.  
  
## Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports<a name="import_data"></a>
Die nachstehenden Beispiele verwenden die oben erstellte Datenbank, Datendatei und Formatdatei.

### **Verwenden von [bcp](../../tools/bcp-utility.md) und Beibehalten von NULL-Werten ohne Formatdatei**<a name="bcp_null"></a>

Schalter**-k** .  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **Verwenden von [bcp](../../tools/bcp-utility.md) und Beibehalten von NULL-Werten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_null_fmt"></a>
Schalter**-k** und **-f** . Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **Verwenden von [bcp](../../tools/bcp-utility.md) und Verwenden von Standardwerten ohne Formatdatei**<a name="bcp_default"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **Verwenden von [bcp](../../tools/bcp-utility.md) und Verwenden von Standardwerten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
Schalter**-f** .  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und Beibehalten von NULL-Werten ohne Formatdatei**<a name="bulk_null"></a>
**KEEPNULLS** -Argument.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
USE TestDatabase;
GO
TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
    FROM 'D:\BCP\myNulls.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und Beibehalten von NULL-Werten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_null_fmt"></a>
**KEEPNULLS** und das Argument **FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt',
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und Verwenden von Standardwerten ohne Formatdatei**<a name="bulk_default"></a>
Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und Verwenden von Standardwerten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und Beibehalten von NULL-Werten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__null_fmt"></a>
Argument**FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und Verwenden von Standardwerten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__default_fmt"></a>
Tabellenhinweis**KEEPDEFAULTS** und Argument **FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
WITH (KEEPDEFAULTS) 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Vorbereiten von Daten für den Massenexport oder -import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **So verwenden Sie eine Formatdatei**  
  
-   [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **So verwenden Sie Datenformate für Massenimport oder Massenexport**  
  
-   [Importieren von Daten aus früheren SQL Server-Versionen im systemeigenen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **So geben Sie Datenformate für die Kompatibilität bei Verwendung von bcp an**  
  
-   [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Angeben der Präfixlänge in Datendateien mittels bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Angeben des Dateispeichertyps mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

