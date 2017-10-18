---
title: Auslassen eines Datenfelds mithilfe einer Formatdatei (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 07658ca2dbba706c7355220349f78b3703fe988e
ms.contentlocale: de-de
ms.lasthandoff: 10/13/2017

---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>Auslassen eines Datenfelds mithilfe einer Formatdatei (SQL Server)
Eine Datendatei kann mehr Felder enthalten, als Spalten in der Tabelle vorhanden sind. In diesem Thema wird beschrieben, wie Nicht-XML- und XML-Formatdateien an eine Datendatei mit mehr Feldern angepasst werden können, indem die Tabellenspalten den entsprechenden Datenfeldern zugeordnet und die übrigen Felder ignoriert werden.  Weitere Informationen finden Sie unter [Erstellen einer Formatdatei (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) .

|Outline|
|---|
|[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispieldatendatei](#sample_data_file)<br />[Erstellen der Formatdateien](#create_format_file)<br />&emsp;&#9679;&emsp;[Erstellen einer Nicht-XML-Formatdatei](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Ändern einer Nicht-XML-Formatdatei](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[Erstellen einer XML-Formatdatei](#xml_format_file)<br />&emsp;&#9679;&emsp;[Ändern einer XML-Formatdatei](#modify_xml_format_file)<br />[Importieren von Daten mithilfe einer Formatdatei zum Überspringen eines Datenfelds](#import_data)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und der Nicht-XML-Formatdatei](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von BCP und der XML-Formatdatei](#bcp_xml)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und der Nicht-XML-Formatdatei](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und der XML-Formatdatei](#bulk_xml)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und der Nicht-XML-Formatdatei](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und der XML-Formatdatei](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
> [!NOTE]
>  Mithilfe einer Nicht-XML- oder XML-Formatdatei kann der Massenimport einer Datendatei in die Tabelle ausgeführt werden. Hierzu kann ein [bcp-Hilfsprogramm](../../tools/bcp-utility.md)-Befehl, eine [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)- oder eine INSERT ... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)-Anweisung verwendet werden. Weitere Informationen finden Sie unter [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).

## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema enthaltenen Beispiele der geänderten Formatdateien basieren auf der Tabelle und der Datendatei, die nachstehend definiert sind.
  
### Beispieltabelle<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank und eine Tabelle namens `myTestSkipField`.  Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
 
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myTestSkipField
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30)
   );
```
  
### Beispieldatendatei<a name="sample_data_file"></a>
Erstellen Sie die leere Datei `D:\BCP\myTestSkipField.bcp` , und fügen Sie die folgenden Daten ein: 
```
1,SkipMe,Anthony,Grosse
2,SkipMe,Alica,Fatnowna
3,SkipMe,Stella,Rosenhain
```
  
## Erstellen der Formatdateien<a name="create_format_file"></a>
Wenn ein Massenimport für Daten aus `myTestSkipField.bcp` in die `myTestSkipField` -Tabelle ausgeführt werden soll, muss die Formatdatei folgende Funktionen ausführen:
* Der ersten Spalte ( `PersonID`) das erste Datenfeld zuordnen.
* Das zweite Datenfeld auslassen.
* Der zweiten Spalte ( `FirstName`) das dritte Datenfeld zuordnen.
* Der dritten Spalte ( `LastName`) das vierte Datenfeld zuordnen.  

Die einfachste Methode zum Erstellen der Formatdatei besteht darin, das [bcp-Dienstprogramm](../../tools/bcp-utility.md)zu verwenden.  Erstellen Sie zunächst eine Basisformatdatei aus der vorhandenen Tabelle.  Ändern Sie dann die Basisformatdatei so, dass sie der tatsächlichen Datendatei entspricht.
  
### <a name="nonxml_format_file"></a>Erstellen einer Nicht-XML-Formatdatei 
Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) . Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myTestSkipField.fmt`zu erstellen, die auf dem Schema von `myTestSkipField`basiert.  Außerdem wird der Qualifizierer `c` verwendet, um Zeichendaten anzugeben, wird `t,` verwendet, um ein Komma als Feldabschlusszeichen anzugeben, und wird `T` verwendet, um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -f D:\BCP\myTestSkipField.fmt -t, -T
```

### Ändern der Nicht-XML-Formatdatei <a name="modify_nonxml_format_file"></a>
Informationen zur Terminologie finden Sie unter [Struktur von Nicht-XML-Formatdateien](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) . Öffnen Sie `D:\BCP\myTestSkipField.fmt` in Editor, und nehmen Sie die folgenden Änderungen vor:
1) Kopieren Sie die gesamte Formatdateizeile für `FirstName` , und fügen Sie sie unmittelbar nach `FirstName` in der nächsten Zeile ein.
2) Setzen Sie den Wert für die Reihenfolge der Felder der Hostdatei für die neue Zeile und alle nachfolgenden Zeilen um eins herauf.
3) Erhöhen Sie den Wert für die Anzahl der Spalten, um die tatsächliche Anzahl der Felder in der Datendatei anzugeben.
3) Ändern Sie die Spaltenreihenfolge auf dem Server für die zweite Zeile der Formatdatei von `2` in `0` . 

Vergleichen Sie die vorgenommenen Änderungen:  
**Vorher**
```
13.0
3
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS
```
**Nach**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      0     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       50      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS

```

Die geänderte Formatdatei berücksichtigt nun:
* 4 Datenfelder
* Das erste Datenfeld in `myTestSkipField.bcp` ist der ersten Spalte zugeordnet, ` myTestSkipField.. PersonID`
* Das zweite Datenfeld in `myTestSkipField.bcp` ist keiner Spalte zugeordnet.
* Das dritte Datenfeld in `myTestSkipField.bcp` ist der zweiten Spalte zugeordnet, `myTestSkipField.. FirstName`
* Das vierte Datenfeld in `myTestSkipField.bcp` ist der dritten Spalte zugeordnet, `myTestSkipField.. LastName`

### Erstellen einer XML-Formatdatei <a name="xml_format_file"></a>  
Ausführliche Informationen finden Sie unter [XML-Formatdateien (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) .  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die XML-Formatdatei `myTestSkipField.xml`zu erstellen, die auf dem Schema von `myTestSkipField`basiert.  Außerdem wird der Qualifizierer `c` verwendet, um Zeichendaten anzugeben, wird `t,` verwendet, um ein Komma als Feldabschlusszeichen anzugeben, und wird `T` verwendet, um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Der `x` -Qualifizierer muss verwendet werden, um eine XML-basierte Formatdatei zu generieren.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -x -f D:\BCP\myTestSkipField.xml -t, -T
```

### Ändern der XML-Formatdatei <a name="modify_xml_format_file"></a>
Informationen zur Terminologie finden Sie unter [Schemasyntax für XML-Formatdateien](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) .  Öffnen Sie `D:\BCP\myTestSkipField.xml` in Editor, und nehmen Sie die folgenden Änderungen vor:
1) Kopieren Sie das gesamte zweite Feld, und fügen Sie es unmittelbar nach dem zweiten Feld in der nächsten Zeile ein.
2) Setzen Sie den Wert von "FIELD ID"für das neue Feld FIELD und für jedes nachfolgende FIELD um 1 herauf.
3) Erhöhen Sie den Wert von "COLUMN SOURCE" für `FirstName`und `LastName` um 1, um der geänderten Zuordnung Rechnung zu tragen.

Vergleichen Sie die vorgenommenen Änderungen:  
**Vorher**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

**Nach**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

Die geänderte Formatdatei berücksichtigt nun:
* 4 Datenfelder
* FIELD 1, das COLUMN 1 entspricht, wird der ersten Tabellenspalte zugeordnet, `myTestSkipField.. PersonID`
* FIELD 2 entspricht keiner COLUMN und wird daher keiner Tabellenspalte zugeordnet.
* FIELD 3, das COLUMN 3 entspricht, wird der zweiten Tabellenspalte zugeordnet, `myTestSkipField.. FirstName`
* FIELD 4, das COLUMN 4 entspricht, wird der dritten Tabellenspalte zugeordnet, `myTestSkipField.. LastName`

## Importieren von Daten mithilfe einer Formatdatei zum Überspringen eines Datenfelds<a name="import_data"></a>
In den folgenden Beispielen werden die Datenbank, die Datendatei und die Formatdateien verwendet, die oben erstellt wurden.

### Verwenden von [bcp](../../tools/bcp-utility.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.fmt -T
```

### Verwenden von [bcp](../../tools/bcp-utility.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.xml -T
```

### Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a>    
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

  
## <a name="see-also"></a>Siehe auch  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  

