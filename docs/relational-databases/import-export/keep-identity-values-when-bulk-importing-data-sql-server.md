---
title: "Beibehalten von Identitätswerten beim Massenimport von Daten (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/21/2016
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
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 95788f86ca16782ed8e51f888004926bf174e950
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>Beibehalten von Identitätswerten beim Massenimport von Daten (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Datendateien, die Identitätswerte enthalten, können per Massenimport in eine Instanz von Microsoft SQL Server übertragen werden.  Standardmäßig werden die Werte für die Identitätsspalte in der importierten Datendatei ignoriert, und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden automatisch eindeutige Werte zugewiesen.  Die eindeutigen Werte basieren auf dem Ausgangswert und den inkrementellen Werten, die bei der Tabellenerstellung angegeben werden.

Wenn die Datendatei keine Werte für die Bezeichnerspalte in der Tabelle enthält, sollten Sie eine Formatdatei verwenden, um anzugeben, dass die Bezeichnerspalte beim Importieren von Daten ausgelassen werden soll.  Weitere Informationen finden Sie unter [Überspringen einer Tabellenspalte mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md) .

|Outline|
|---|
|[Beibehalten von Identitätswerten](#keep_identity)<br />[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispieldatendatei](#sample_data_file)<br />&emsp;&#9679;&emsp;[Beispiel einer Nicht-XML-Formatdatei](#nonxml_format_file)<br />[Beispiele](#examples)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und Beibehalten der Identitätswerte ohne Formatdatei](#bcp_identity)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und Beibehalten der Identitätswerte mit einer Nicht-XML-Formatdatei](#bcp_identity_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und generierten Identitätswerten ohne Formatdatei](#bcp_default)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und generierten Identitätswerten mit einer Nicht-XML-Formatdatei](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und Beibehalten der Identitätswerte ohne Formatdatei](#bulk_identity)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und Beibehalten der Identitätswerte mit einer Nicht-XML-Formatdatei](#bulk_identity_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und generierten Identitätswerten ohne Formatdatei](#bulk_default)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und generierten Identitätswerten mit einer Nicht-XML-Formatdatei](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET und Beibehalten der Identitätswerte mit einer Nicht-XML-Formatdatei](#openrowset_identity_fmt)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET und generierten Identitätswerten mit einer Nicht-XML-Formatdatei](#openrowset_default_fmt)<br /><p>                                                                                                                                                                                                                  </p>|

## Beibehalten von Identitätswerten <a name="keep_identity"></a>  
Um zu verhindern, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Massenimport von Datenzeilen in eine Tabelle Identitätswerte zuweist, verwenden Sie den entsprechenden Qualifizierer für den Befehl zur Identitätsbeibehaltung (keepidentity).  Wenn Sie einen Qualifizierer zur Identitätsbeibehaltung angeben, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Identitätswerte in der Datendatei.  Nachfolgend sind diese Qualifizierer aufgeführt:

|Befehl|Qualifizierer zur Identitätsbeibehaltung|Qualifizierertyp|  
|-------------|------------------------------|--------------------|  
|bcp|-E|Schalter|  
|BULK INSERT|KEEPIDENTITY|Argument|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|Tabellenhinweis|  
   
 Weitere Informationen finden Sie unter [bcp (Hilfsprogramm)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md), [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) und [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  

> [!NOTE]
>  Weitere Informationen zu einer automatisch inkrementierten Zahl, die in mehreren Tabellen verwendet oder aus Anwendungen aufgerufen werden kann, ohne dass auf eine Tabelle verwiesen wird, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).
 
## Beispiel-Testbedingungen<a name="etc"></a>  
Die in diesem Thema beschriebenen Beispiele basieren auf einer Tabelle, einer Datendatei und einer Formatdatei, die nachstehend definiert werden.

### **Beispieltabelle**<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank und eine Tabelle namens `myIdentity`.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myIdentity ( 
   PersonID smallint IDENTITY(1,1) NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date
   );
```
 
### **Beispieldatendatei**<a name="sample_data_file"></a>
Erstellen Sie im Editor die leere Datei `D:\BCP\myIdentity.bcp` , und fügen Sie die nachstehenden Daten ein.  
```
3,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
1,Stella,Rosenhain,1992-03-02
4,Miller,Dylan,1954-01-05
```
  
Alternativ können Sie das folgende PowerShell-Skript ausführen, um die Datei zu erstellen und aufzufüllen:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'myIdentity.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '3,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '1,Stella,Rosenhain,1992-03-02';
Add-Content -Path $bcpFile -Value '4,Miller,Dylan,1954-01-05';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

### **Beispiel einer Nicht-XML-Formatdatei**<a name="nonxml_format_file"></a>
SQL Server unterstützt zwei Typen von Formatdateien: Nicht-XML- und XML-Format.  Nicht-XML ist das ursprüngliche Format, das von früheren Versionen von SQL Server unterstützt wird.  Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myIdentity.fmt`zu erstellen, die auf dem Schema von `myIdentity`basiert.  Geben Sie bei der Ausführung eines [bcp](../../tools/bcp-utility.md) -Befehls zum Erstellen einer Formatdatei das **format** -Argument an, und verwenden Sie **nul** anstatt eines Datendateipfads.  Die Option „format“ erfordert außerdem die Option **-f** .  Zusätzlich werden folgende Qualifizierer verwendet: **c** , um Zeichendaten anzugeben, **t** , um ein Komma als [Feldabschlusszeichen](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)anzugeben, und **T** , um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
  
```
bcp TestDatabase.dbo.myIdentity format nul -c -f D:\BCP\myIdentity.fmt -t, -T

REM Review file
Notepad D:\BCP\myIdentity.fmt
```
 
> [!IMPORTANT]
> Stellen Sie sicher, dass Ihre Nicht-XML-Formatdatei mit einem Wagenrücklauf/Zeilenvorschub endet.  Andernfalls wird Ihnen möglicherweise die folgende Fehlermeldung angezeigt:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Beispiele<a name="examples"></a>
Die nachstehenden Beispiele verwenden die oben erstellte Datenbank, Datendatei und Formatdatei.
  
### **Verwenden von [bcp](../../tools/bcp-utility.md) und Beibehalten der Identitätswerte ohne Formatdatei**<a name="bcp_identity"></a>
Schalter**-E** .  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t, -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```

### **Verwenden von [bcp](../../tools/bcp-utility.md) und Beibehalten der Identitätswerte mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_identity_fmt"></a>
Schalter**-E** und **-f** .  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
 
### **Verwenden von [bcp](../../tools/bcp-utility.md) und generierten Identitätswerten ohne Formatdatei**<a name="bcp_default"></a>
Unter Verwendung der Standardeinstellungen.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t,

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Verwenden von [bcp](../../tools/bcp-utility.md) und generierten Identitätswerten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
Verwenden Sie die Standardeinstellungen und den Schalter **-f** .  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und Beibehalten der Identitätswerte ohne Formatdatei**<a name="bulk_identity"></a>
Argument**KEEPIDENTITY** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
    FROM 'D:\BCP\myIdentity.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und Beibehalten der Identitätswerte mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_identity_fmt"></a>
Argumente**KEEPIDENTITY** und **FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt',
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und generierten Identitätswerten ohne Formatdatei**<a name="bulk_default"></a>
Unter Verwendung der Standardeinstellungen.  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und generierten Identitätswerten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
Verwenden Sie die Standardwerte und das Argument **FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und Beibehalten der Identitätswerte mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_identity_fmt"></a>
Tabellenhinweis**KEEPIDENTITY** und Argument **FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
WITH (KEEPIDENTITY) 
(PersonID, FirstName, LastName, BirthDate)
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
 
### **Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und generierten Identitätswerten mit einer [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_default_fmt"></a>
Verwenden Sie die Standardwerte und das Argument **FORMATFILE** .  Führen Sie den folgenden Transact-SQL-Befehl in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
(FirstName, LastName, BirthDate)
    SELECT FirstName, LastName, BirthDate
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
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
  
1.  [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
2.  [Angeben der Präfixlänge in Datendateien mittels bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Angeben des Dateispeichertyps mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
[Formatdateien zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
