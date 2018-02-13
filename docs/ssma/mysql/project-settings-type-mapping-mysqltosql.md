---
title: Projekteinstellungen (Zuordnung) (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ca62e82b85d401f99a6e59f6f440d9a6519e58d
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="project-settings-type-mapping-mysqltosql"></a>Projekteinstellungen (Zuordnung) (MySQLToSQL)
Die projekteinstellungen Type Mapping können Sie die standardtypmappings für das SSMA-Projekt festgelegt.  

Zuordnung ist in den Dialogfeldern Projekteinstellungen und Projekt Standardeinstellungen verfügbar:  
  
-   Verwenden Sie das Dialogfeld Projekteinstellungen, um Konfigurationsoptionen für das aktuelle Projekt festzulegen. Für den Zugriff auf die Einstellungen für Zuordnung, klicken Sie im Menü Extras, wählen Sie die Einstellungen für Projektdateien, und klicken Sie dann im linken Bereich auf Typzuordnung.  
  
-   Verwenden Sie das Dialogfeld Projekt Standardeinstellungen, um Konfigurationsoptionen für alle Projekte festzulegen. Wählen Sie die Zuordnung Zugriff auf Einstellungen, klicken Sie im Menü Extras, Projekteinstellungen Default, select Migration-Projekttyp, die für die Einstellungen angezeigt oder geändert werden, erforderlich sind **Migration Zielversion** Dropdown-Liste, und klicken Sie dann im linken Bereich auf Typzuordnung.  
  
## <a name="options"></a>enthalten  
  
##### <a name="source-type"></a>Quelltyp  
Es wird die MySQL-Datentyp, der in den Zieldatentyp der Datenbank zugeordnet werden muss.  
  
##### <a name="target-type"></a>Zieltyp  
Geben Sie die Zieldaten für die Datenbank für den angegebenen MySQL-Datentyp.  
  
##### <a name="add"></a>Hinzufügen  
Klicken Sie auf diese Option, um einen Datentyp der Zuordnungsliste hinzuzufügen.  
  
##### <a name="edit"></a>Bearbeiten  
Klicken Sie auf diese Option, um den ausgewählten Datentyp in der Zuordnungsliste zu bearbeiten.  
  
##### <a name="remove"></a>Entfernen  
Klicken Sie auf diese Option, um die ausgewählte Zuordnung aus der Zuordnungsliste zu entfernen.  
  
##### <a name="reset-to-default"></a>Standard wiederherstellen  
Klicken Sie auf diese Option, um die Liste ' datentypzuordnung ' auf die SSMA-Standardwerte zurückzusetzen.  
  
## <a name="type-mappings"></a>Datentypzuordnungen  
Die folgende Tabelle zeigt die Zuordnung zwischen Quelle und Ziel-Datentypen  
  
|||  
|-|-|  
|**MySQL-Datentyp**|**SQL Server-Datentyp**|  
|bigint|bigint|  
|"bigint" [*.. 255]|bigint|  
|BINARY|Binär [1]|  
|Binär [0.. 1]|Binär [1]|  
|Binär [2..255]|Binär [*]|  
|bit|Binär [1]|  
|Bit [0..8]|Binär [1]|  
|Bit [17..24]|binary[3]|  
|Bit [25..32]|Binär [4]|  
|bit[33..40]|Binär [5]|  
|Bit [41..48]|binary[6]|  
|Bit [49..56]|Binär [7]|  
|Bit [57..64]|binary[8]|  
|Bit [9..16]|Binär [2]|  
|Blob|varbinary(max)|  
|BLOB [0.. 1]|varbinary[1]|  
|BLOB [2..8000]|varbinary[*]|  
|blob[8001..*]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar[1]|  
|Char-byte|Binär [1]|  
|Char Byte [0.. 1]|Binär [1]|  
|Char Byte [2..255]|Binär [*]|  
|Char [0.. 1]|nchar[1]|  
|Char [2..255]|nchar[*]|  
|character|nchar[1]|  
|Zeichen, die unterschiedliche [0.. 1]|nvarchar[1]|  
|Zeichen, die unterschiedliche [2..255]|nvarchar|  
|Zeichen [0.. 1]|nchar[1]|  
|Zeichen [2..255]|nchar[*]|  
|Datum|Datum|  
|datetime|datetime2 [0]|  
|dec|Decimal|  
|DEC [*.. 65]|Dezimal [*] [0]|  
|dec[*..65][\*..30]|decimal[*][\*]|  
|Decimal|Decimal|  
|Dezimal [*.. 65]|Dezimal [*] [0]|  
|Dezimal [*.. 65][\*.. 30]|decimal[*][\*]|  
|double|float[53]|  
|mit doppelter Genauigkeit|float[53]|  
|doppelte Genauigkeit [*.. 255][\*.. 30]|numeric[*][\*]|  
|Doppelte [*.. 255][\*.. 30]|numeric[*][\*]|  
|feste|numeric|  
|feste [*.. 65][\*.. 30]|numeric[*][\*]|  
|float|float[24]|  
|float[*..255][\*..30]|numeric[*][\*]|  
|"float" [*.. 53]|float[53]|  
|int|int|  
|Int [*.. 255]|int|  
|integer|int|  
|ganze Zahl [*.. 255]|int|  
|longblob|varbinary(max)|  
|LONGTEXT|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint[*..255]|int|  
|mediumtext|nvarchar(max)|  
|National char|nchar[1]|  
|National Char [0.. 1]|nchar[1]|  
|National Char [2..255]|nchar[*]|  
|nationale Zeichensätze|nchar[1]|  
|nationale Zeichensätze varying|nvarchar[1]|  
|nationale Zeichensätze, die unterschiedliche [0.. 1]|nvarchar[1]|  
|nationale Zeichensätze, die unterschiedliche [2..4000]|nvarchar[*]|  
|nationale Zeichensätze varying [4001.. *]|nvarchar(max)|  
|nationale Zeichensätze [0.. 1]|nchar[1]|  
|nationale Zeichensätze [2..255]|nchar[*]|  
|National varchar|nvarchar[1]|  
|National Varchar [0.. 1]|nvarchar[1]|  
|National Varchar [2..4000]|nvarchar[*]|  
|National Varchar [4001.. *]|nvarchar(max)|  
|NCHAR|nchar[1]|  
|NCHAR varchar|nvarchar[1]|  
|Nchar, Varchar [0.. 1]|nvarchar[1]|  
|Nchar, Varchar [2..4000]|nvarchar[*]|  
|NCHAR Varchar [4001.. *]|nvarchar(max)|  
|NCHAR [0.. 1]|nchar[1]|  
|NCHAR [2..255]|nchar[*]|  
|numeric|numeric|  
|numerische [*.. 65]|numeric[*][0]|  
|numeric[*..65][\*..30]|numeric[*][\*]|  
|nvarchar|nvarchar[1]|  
|Nvarchar [0.. 1]|nvarchar[1]|  
|Nvarchar [2..4000]|nvarchar[*]|  
|nvarchar[4001..*]|nvarchar(max)|  
|real|float[53]|  
|real[*..255][\*..30]|numeric[*][\*]|  
|Serielle|bigint|  
|smallint|smallint|  
|"smallint" [*.. 255]|smallint|  
|text|nvarchar(max)|  
|Text [0.. 1]|nvarchar[1]|  
|Text [2..4000]|nvarchar[*]|  
|text[4001..*]|nvarchar(max)|  
|Uhrzeit|Uhrzeit|  
|timestamp|datetime|  
|tinyblob|varbinary[255]|  
|tinyint|smallint|  
|"tinyint" [*.. 255]|smallint|  
|tinytext|nvarchar[255]|  
|ohne Vorzeichen "bigint"|bigint|  
|ohne Vorzeichen "bigint" [*.. 255]|bigint|  
|ohne Vorzeichen Dez.|Decimal|  
|ohne Vorzeichen Dec [*.. 65]|Dezimal [*] [0]|  
|ohne Vorzeichen Dec [*.. 65][\*.. 30]|decimal[*][\*]|  
|Dezimalzahl ohne Vorzeichen|Decimal|  
|Dezimalzahl ohne Vorzeichen [*.. 65]|Dezimal [*] [0]|  
|Dezimalzahl ohne Vorzeichen [*.. 65][\*.. 30]|decimal[*][\*]|  
|Doppelte ohne Vorzeichen|float[53]|  
|ohne Vorzeichen mit doppelter Genauigkeit|float[53]|  
|ohne Vorzeichen mit doppelter Genauigkeit [*.. 255][\*.. 30]|numeric[*][\*]|  
|nicht signierte double [*.. 255][\*.. 30]|numeric[*][\*]|  
|feste unsigniert|numeric|  
|nicht signierte festen [*.. 65][\*.. 30]|numeric[*][\*]|  
|ohne Vorzeichen "float"|float[24]|  
|ohne Vorzeichen "float" [*.. 255][\*.. 30]|numeric[*][\*]|  
|ohne Vorzeichen "float" [*.. 53]|float[53]|  
|Int ohne Vorzeichen|bigint|  
|Int ohne Vorzeichen [*.. 255]|bigint|  
|ganze Zahl ohne Vorzeichen|bigint|  
|ganze Zahl ohne Vorzeichen [*.. 255]|bigint|  
|ohne Vorzeichen mediumint|int|  
|ohne Vorzeichen Mediumint [*.. 255]|int|  
|ohne Vorzeichen numerisch|numeric|  
|ohne Vorzeichen numerische [*.. 65]|numeric[*][0]|  
|ohne Vorzeichen numerische [*.. 65][\*.. 30]|numeric[*][\*]|  
|real ohne Vorzeichen|float[53]|  
|real unsigniert [*.. 255[[\*.. 30]|numeric[*][\*]|  
|ohne Vorzeichen "smallint"|int|  
|ohne Vorzeichen "smallint" [*.. 255]|int|  
|ohne Vorzeichen "tinyint"|tinyint|  
|ohne Vorzeichen "tinyint" [*.. 255]|tinyint|  
|Varbinary [0.. 1]|varbinary[1]|  
|Varbinary [2..8000]|varbinary[*]|  
|varbinary[8001..*]|varbinary(max)|  
|Varchar [0.. 1]|nvarchar[1]|  
|Varchar [2..4000]|nvarchar[*]|  
|Varchar [4001.. *]|nvarchar(max)|  
|Jahr|smallint|  
|Jahr [2..2]|smallint|  
|Jahr [4..4]|smallint|  
  
##### <a name="add"></a>Hinzufügen  
Klicken Sie auf diese Option, um einen Datentyp der Zuordnungsliste hinzuzufügen.  
  
##### <a name="edit"></a>Bearbeiten  
Klicken Sie auf diese Option, um einen Datentyp in der Zuordnungsliste zu bearbeiten.  
  
##### <a name="remove"></a>Entfernen  
Klicken Sie auf diese Option, um die ausgewählte Zuordnung aus der Zuordnungsliste zu entfernen.  
  
##### <a name="reset-to-default"></a>Standard wiederherstellen  
Klicken Sie auf diese Option, um alle datentypzuordnungen auf die SSMA-Standardwerte zurückzusetzen.  
  
