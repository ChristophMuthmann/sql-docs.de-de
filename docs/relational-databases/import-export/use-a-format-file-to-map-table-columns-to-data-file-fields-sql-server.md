---
title: "Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "09/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Zuordnen von Spalten zu Feldern beim Import [SQL Server]"
  - "Formatdateien [SQL Server], Zuordnen von Spalten zu Feldern"
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
caps.latest.revision: 40
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 40
---
# Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern (SQL Server)
Eine Datendatei kann Felder in einer anderen Reihenfolge als die der entsprechenden Spalten in der Tabelle aufweisen. In diesem Thema werden Nicht-XML-Formatdateien und XML-Formatdateien dargestellt, die zum Anpassen an eine Datendatei, deren Felder eine andere Reihenfolge als die Tabellenspalten aufweisen, geändert wurden. Die geänderte Formatdatei ordnet die Datenfelder den entsprechenden Tabellenspalten zu.  Weitere Informationen finden Sie unter [Erstellen einer Formatdatei (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md).

|Outline|
|---|
|[Beispieltestbedingungen](#etc)<br />&emsp;&#9679;&emsp;[Beispieltabelle](#sample_table)<br />&emsp;&#9679;&emsp;[Beispieldatendatei](#sample_data_file)<br />[Erstellen der Formatdateien](#create_format_file)<br />&emsp;&#9679;&emsp;[Erstellen einer Nicht-XML-Formatdatei](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Ändern der Nicht-XML-Formatdatei](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[Erstellen einer XML-Formatdatei](#xml_format_file)<br />&emsp;&#9679;&emsp;[Ändern der XML-Formatdatei](#modify_xml_format_file)<br />[Importieren von Daten mit einer Formatdatei, um Tabellenspalten zu Datendateifeldern zuzuordnen](#import_data)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und der Nicht-XML-Formatdatei](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von bcp und der XML-Formatdatei](#bcp_xml)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und der Nicht-XML-Formatdatei](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von BULK INSERT und der XML-Formatdatei](#bulk_xml)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und der Nicht-XML-Formatdatei](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Verwenden von OPENROWSET(BULK...) und der XML-Formatdatei](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|

> [!NOTE]  
>  Mithilfe einer Nicht-XML- oder XML-Formatdatei kann der Massenimport einer Datendatei in die Tabelle ausgeführt werden. Hierzu kann ein [bcp-Hilfsprogramm](../../tools/bcp-utility.md)-Befehl, eine [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)- oder eine INSERT ... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)-Anweisung verwendet werden. Weitere Informationen finden Sie unter [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

## Beispieltestbedingungen<a name="etc"></a>  
Die in diesem Thema enthaltenen Beispiele der geänderten Formatdateien basieren auf der Tabelle und der Datendatei, die nachstehend definiert sind.

### Beispieltabelle<a name="sample_table"></a>
Das folgende Skript erstellt eine Testdatenbank und eine Tabelle namens `myRemap`.  Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myRemap
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   Gender char(1)
   );
```

### Beispieldatendatei<a name="sample_data_file"></a>
Die nachstehenden Daten entsprechen `FirstName` und `LastName` in umgekehrter Reihenfolge, wie in der Tabelle `myRemap` dargestellt.  Erstellen Sie mit Editor die leere Datei `D:\BCP\myRemap.bcp`, und fügen Sie die folgenden Daten ein:
```
1,Grosse,Anthony,M
2,Fatnowna,Alica,F
3,Rosenhain,Stella,F
```

## Erstellen der Formatdateien<a name="create_format_file"></a>
Wenn ein Massenimport für Daten aus `myRemap.bcp` in die `myRemap`-Tabelle ausgeführt werden soll, muss die Formatdatei folgende Funktionen ausführen:
* Der ersten Spalte ( `PersonID`) das erste Datenfeld zuordnen.
* Der dritten Spalte (`LastName`) das zweite Datenfeld zuordnen.
* Der zweiten Spalte ( `FirstName`) das dritte Datenfeld zuordnen.
* Der vierten Spalte (`Gender`) das vierte Datenfeld zuordnen.

Die einfachste Methode zum Erstellen der Formatdatei besteht darin, das [bcp-Dienstprogramm](../../tools/bcp-utility.md) zu verwenden.  Erstellen Sie zunächst eine Basisformatdatei aus der vorhandenen Tabelle.  Ändern Sie dann die Basisformatdatei so, dass sie der tatsächlichen Datendatei entspricht.

### Erstellen einer Nicht-XML-Formatdatei<a name="nonxml_format_file"></a>
Ausführliche Informationen finden Sie unter [Nicht-XML-Formatdateien (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md). Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die Nicht-XML-Formatdatei `myRemap.fmt` zu erstellen, die auf dem Schema von `myRemap` basiert.  Außerdem wird der Qualifizierer `c` verwendet, um Zeichendaten anzugeben, wird `t,` verwendet, um ein Komma als Feldabschlusszeichen anzugeben, und wird `T` verwendet, um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myRemap format nul -c -f D:\BCP\myRemap.fmt -t, -T
```
### Ändern der Nicht-XML-Formatdatei <a name="modify_nonxml_format_file"></a>
Informationen zur Terminologie finden Sie unter [Struktur von Nicht-XML-Formatdateien](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure).  Öffnen Sie `D:\BCP\myRemap.fmt` in Editor, und nehmen Sie die folgenden Änderungen vor:
1) Ändern Sie die Reihenfolge der Zeilen in der Formatdatei, sodass die Zeilen in derselben Reihenfolge vorliegen wie die Daten in `myRemap.bcp`.
2) Stellen Sie sicher, dass die Werte für die Reihenfolge der Hostfelder sequenziell sind.
3) Stellen Sie sicher, dass nach der letzten Zeile der Formatdatei ein Zeilenumbruch eingefügt wird.

Vergleichen Sie die Änderungen:     
**vor**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID               ""
2       SQLCHAR 0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
**Nach**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID               ""
2       SQLCHAR 0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
Die geänderte Formatdatei entspricht nun Folgendem:
* Das erste Datenfeld in `myRemap.bcp` wird der ersten Spalte zugeordnet, ` myRemap.. PersonID`
* Das zweite Datenfeld in `myRemap.bcp` wird der dritten Spalte zugeordnet, `myRemap.. LastName`
* Das dritte Datenfeld in `myRemap.bcp` wird der zweiten Spalte zugeordnet, `myRemap.. FirstName`
* Das vierte Datenfeld in `myRemap.bcp` wird der vierten Spalte zugeordnet, ` myRemap.. Gender`

### Erstellen einer XML-Formatdatei <a name="xml_format_file"></a>  
Ausführliche Informationen finden Sie unter [XML-Formatdateien (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md).  Im folgenden Befehl wird das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) verwendet, um die XML-Formatdatei `myRemap.xml` zu erstellen, die auf dem Schema von `myRemap` basiert.  Außerdem wird der Qualifizierer `c` verwendet, um Zeichendaten anzugeben, wird `t,` verwendet, um ein Komma als Feldabschlusszeichen anzugeben, und wird `T` verwendet, um eine vertrauenswürdige Verbindung anzugeben, für die integrierte Sicherheit verwendet wird.  Der `x`-Qualifizierer muss verwendet werden, um eine XML-basierte Formatdatei zu generieren.  Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myRemap format nul -c -x -f D:\BCP\myRemap.xml -t, -T
```
### Ändern der XML-Formatdatei <a name="modify_xml_format_file"></a>
Informationen zur Terminologie finden Sie unter [Schemasyntax für XML-Formatdateien](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs).  Öffnen Sie `D:\BCP\myRemap.xml` in Editor, und nehmen Sie die folgenden Änderungen vor:
1) Die Reihenfolge, in der die \<FIELD>-Elemente in der Formatdatei deklariert sind, ist die Reihenfolge, in der diese Felder in der Datendatei angezeigt werden. Kehren Sie daher die Reihenfolge für die \<FIELD>-Elemente mit den ID-Attributen 2 und 3 um.
2) Stellen Sie sicher, dass die Werte des \<FIELD>-Attributs ID sequenziell sind.
3) Die Reihenfolge der \<COLUMN>-Elemente im \<ROW>-Element definiert, in welcher Reihenfolge diese durch den Massenvorgang zurückgegeben werden.  Die XML-Formatdatei weist jedem \<COLUMN>-Element einen lokalen Namen zu, der keine Verbindung zu der Spalte in der Zieltabelle des Massenimportvorgangs aufweist.  Die Reihenfolge der \<COLUMN>-Elemente ist unabhängig von der Reihenfolge der \<FIELD>-Elemente in einer \<RECORD>-Definition.  Jedes \<COLUMN>-Element entspricht einem \<FIELD>-Element (dessen ID im SOURCE-Attribut des \<COLUMN>-Elements angegeben ist).  Somit sind die Werte für \<COLUMN> SOURCE die einzigen Attribute, die eine Überarbeitung erfordern.  Kehren Sie die Reihenfolge für die \<COLUMN>-Attribute SOURCE 2 und 3 um.

Vergleichen Sie die Änderungen:  
**vor**
```
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
**Nach**
```
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="2" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
Die geänderte Formatdatei entspricht nun Folgendem:
* FIELD 1, das COLUMN 1 entspricht, wird der ersten Tabellenspalte zugeordnet, `myRemap.. PersonID`
* FIELD 2, das COLUMN 2 entspricht, wird der dritten Tabellenspalte neu zugeordnet, `myRemap.. LastName`
* FIELD 3, das COLUMN 3 entspricht, wird der zweitten Tabellenspalte neu zugeordnet, `myRemap.. FirstName`
* FIELD 4, das COLUMN 4 entspricht, wird der vierten Tabellenspalte zugeordnet, `myRemap.. Gender`


## Importieren von Daten mit einer Formatdatei, um Tabellenspalten zu Datendateifeldern zuzuordnen<a name="import_data"></a>
In den folgenden Beispielen werden die Datenbank, die Datendatei und die Formatdateien verwendet, die oben erstellt wurden.

### Verwenden von [bcp](../../tools/bcp-utility.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.fmt -T
```

### Verwenden von [bcp](../../tools/bcp-utility.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
Geben Sie folgenden Befehl an der Eingabeaufforderung ein:
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.xml -T
```

### Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Verwenden von [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und der [Nicht-XML-Formatdatei](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a> 
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Verwenden von [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) und der [XML-Formatdatei](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
Führen Sie die folgenden Transact-SQL-Anweisungen in Microsoft SQL Server Management Studio (SSMS) aus:
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```


  
## Siehe auch  
[bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  