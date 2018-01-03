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
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ca62e82b85d401f99a6e59f6f440d9a6519e58d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-type-mapping-mysqltosql"></a>Projekteinstellungen (Zuordnung) (MySQLToSQL)
Die projekteinstellungen Type Mapping können Sie die standardtypmappings für das SSMA-Projekt festgelegt.  

Zuordnung ist in den Dialogfeldern Projekteinstellungen und Projekt Standardeinstellungen verfügbar:  
  
-   Verwenden Sie das Dialogfeld Projekteinstellungen, um Konfigurationsoptionen für das aktuelle Projekt festzulegen. Für den Zugriff auf die Einstellungen für Zuordnung, klicken Sie im Menü Extras, wählen Sie die Einstellungen für Projektdateien, und klicken Sie dann im linken Bereich auf Typzuordnung.  
  
-   Verwenden Sie das Dialogfeld Projekt Standardeinstellungen, um Konfigurationsoptionen für alle Projekte festzulegen. Wählen Sie die Zuordnung Zugriff auf Einstellungen, klicken Sie im Menü Extras, Projekteinstellungen Default, select Migration-Projekttyp, die für die Einstellungen angezeigt oder geändert werden, erforderlich sind **Migration Zielversion** Dropdown-Liste, und klicken Sie dann im linken Bereich auf Typzuordnung.  
  
## <a name="options"></a>Tastatur  
  
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
|BIGINT|BIGINT|  
|"bigint" [*.. 255]|BIGINT|  
|BINARY|Binär [1]|  
|Binär [0.. 1]|Binär [1]|  
|Binär [2..255]|Binär [*]|  
|bit|Binär [1]|  
|Bit [0..8]|Binär [1]|  
|Bit [17..24]|Binär [3]|  
|Bit [25..32]|Binär [4]|  
|Bit [33..40]|Binär [5]|  
|Bit [41..48]|Binär [6]|  
|Bit [49..56]|Binär [7]|  
|Bit [57..64]|Binär [8]|  
|Bit [9..16]|Binär [2]|  
|Blob|varbinary(max)|  
|BLOB [0.. 1]|Varbinary [1]|  
|BLOB [2..8000]|Varbinary [*]|  
|BLOB [8001.. *]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|NCHAR [1]|  
|Char-byte|Binär [1]|  
|Char Byte [0.. 1]|Binär [1]|  
|Char Byte [2..255]|Binär [*]|  
|Char [0.. 1]|NCHAR [1]|  
|Char [2..255]|NCHAR [*]|  
|character|NCHAR [1]|  
|Zeichen, die unterschiedliche [0.. 1]|Nvarchar [1]|  
|Zeichen, die unterschiedliche [2..255]|NVARCHAR|  
|Zeichen [0.. 1]|NCHAR [1]|  
|Zeichen [2..255]|NCHAR [*]|  
|date|date|  
|DATETIME|datetime2 [0]|  
|dec|Decimal|  
|DEC [*.. 65]|Dezimal [*] [0]|  
|DEC [*.. 65][\*.. 30]|Dezimal [*] [\*]|  
|Decimal|Decimal|  
|Dezimal [*.. 65]|Dezimal [*] [0]|  
|Dezimal [*.. 65][\*.. 30]|Dezimal [*] [\*]|  
|double|"float" [53]|  
|mit doppelter Genauigkeit|"float" [53]|  
|doppelte Genauigkeit [*.. 255][\*.. 30]|numerische [*] [\*]|  
|Doppelte [*.. 255][\*.. 30]|numerische [*] [\*]|  
|feste|NUMERIC|  
|feste [*.. 65][\*.. 30]|numerische [*] [\*]|  
|FLOAT|"float" [24]|  
|"float" [*.. 255][\*.. 30]|numerische [*] [\*]|  
|"float" [*.. 53]|"float" [53]|  
|ssNoversion|ssNoversion|  
|Int [*.. 255]|ssNoversion|  
|integer|ssNoversion|  
|ganze Zahl [*.. 255]|ssNoversion|  
|longblob|varbinary(max)|  
|LONGTEXT|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|ssNoversion|  
|Mediumint [*.. 255]|ssNoversion|  
|mediumtext|nvarchar(max)|  
|National char|NCHAR [1]|  
|National Char [0.. 1]|NCHAR [1]|  
|National Char [2..255]|NCHAR [*]|  
|nationale Zeichensätze|NCHAR [1]|  
|nationale Zeichensätze varying|Nvarchar [1]|  
|nationale Zeichensätze, die unterschiedliche [0.. 1]|Nvarchar [1]|  
|nationale Zeichensätze, die unterschiedliche [2..4000]|Nvarchar [*]|  
|nationale Zeichensätze varying [4001.. *]|nvarchar(max)|  
|nationale Zeichensätze [0.. 1]|NCHAR [1]|  
|nationale Zeichensätze [2..255]|NCHAR [*]|  
|National varchar|Nvarchar [1]|  
|National Varchar [0.. 1]|Nvarchar [1]|  
|National Varchar [2..4000]|Nvarchar [*]|  
|National Varchar [4001.. *]|nvarchar(max)|  
|NCHAR|NCHAR [1]|  
|NCHAR varchar|Nvarchar [1]|  
|Nchar, Varchar [0.. 1]|Nvarchar [1]|  
|Nchar, Varchar [2..4000]|Nvarchar [*]|  
|NCHAR Varchar [4001.. *]|nvarchar(max)|  
|NCHAR [0.. 1]|NCHAR [1]|  
|NCHAR [2..255]|NCHAR [*]|  
|NUMERIC|NUMERIC|  
|numerische [*.. 65]|numerische [*] [0]|  
|numerische [*.. 65][\*.. 30]|numerische [*] [\*]|  
|NVARCHAR|Nvarchar [1]|  
|Nvarchar [0.. 1]|Nvarchar [1]|  
|Nvarchar [2..4000]|Nvarchar [*]|  
|Nvarchar [4001.. *]|nvarchar(max)|  
|REAL|"float" [53]|  
|echte [*.. 255][\*.. 30]|numerische [*] [\*]|  
|Serielle|BIGINT|  
|SMALLINT|SMALLINT|  
|"smallint" [*.. 255]|SMALLINT|  
|text|nvarchar(max)|  
|Text [0.. 1]|Nvarchar [1]|  
|Text [2..4000]|Nvarchar [*]|  
|Text [4001.. *]|nvarchar(max)|  
|Uhrzeit|Uhrzeit|  
|timestamp|DATETIME|  
|tinyblob|Varbinary [255]|  
|TINYINT|SMALLINT|  
|"tinyint" [*.. 255]|SMALLINT|  
|tinytext|Nvarchar [255]|  
|ohne Vorzeichen "bigint"|BIGINT|  
|ohne Vorzeichen "bigint" [*.. 255]|BIGINT|  
|ohne Vorzeichen Dez.|Decimal|  
|ohne Vorzeichen Dec [*.. 65]|Dezimal [*] [0]|  
|ohne Vorzeichen Dec [*.. 65][\*.. 30]|Dezimal [*] [\*]|  
|Dezimalzahl ohne Vorzeichen|Decimal|  
|Dezimalzahl ohne Vorzeichen [*.. 65]|Dezimal [*] [0]|  
|Dezimalzahl ohne Vorzeichen [*.. 65][\*.. 30]|Dezimal [*] [\*]|  
|Doppelte ohne Vorzeichen|"float" [53]|  
|ohne Vorzeichen mit doppelter Genauigkeit|"float" [53]|  
|ohne Vorzeichen mit doppelter Genauigkeit [*.. 255][\*.. 30]|numerische [*] [\*]|  
|nicht signierte double [*.. 255][\*.. 30]|numerische [*] [\*]|  
|feste unsigniert|NUMERIC|  
|nicht signierte festen [*.. 65][\*.. 30]|numerische [*] [\*]|  
|ohne Vorzeichen "float"|"float" [24]|  
|ohne Vorzeichen "float" [*.. 255][\*.. 30]|numerische [*] [\*]|  
|ohne Vorzeichen "float" [*.. 53]|"float" [53]|  
|Int ohne Vorzeichen|BIGINT|  
|Int ohne Vorzeichen [*.. 255]|BIGINT|  
|ganze Zahl ohne Vorzeichen|BIGINT|  
|ganze Zahl ohne Vorzeichen [*.. 255]|BIGINT|  
|ohne Vorzeichen mediumint|ssNoversion|  
|ohne Vorzeichen Mediumint [*.. 255]|ssNoversion|  
|ohne Vorzeichen numerisch|NUMERIC|  
|ohne Vorzeichen numerische [*.. 65]|numerische [*] [0]|  
|ohne Vorzeichen numerische [*.. 65][\*.. 30]|numerische [*] [\*]|  
|real ohne Vorzeichen|"float" [53]|  
|real unsigniert [*.. 255[[\*.. 30]|numerische [*] [\*]|  
|ohne Vorzeichen "smallint"|ssNoversion|  
|ohne Vorzeichen "smallint" [*.. 255]|ssNoversion|  
|ohne Vorzeichen "tinyint"|TINYINT|  
|ohne Vorzeichen "tinyint" [*.. 255]|TINYINT|  
|Varbinary [0.. 1]|Varbinary [1]|  
|Varbinary [2..8000]|Varbinary [*]|  
|Varbinary [8001.. *]|varbinary(max)|  
|Varchar [0.. 1]|Nvarchar [1]|  
|Varchar [2..4000]|Nvarchar [*]|  
|Varchar [4001.. *]|nvarchar(max)|  
|Jahr|SMALLINT|  
|Jahr [2..2]|SMALLINT|  
|Jahr [4..4]|SMALLINT|  
  
##### <a name="add"></a>Hinzufügen  
Klicken Sie auf diese Option, um einen Datentyp der Zuordnungsliste hinzuzufügen.  
  
##### <a name="edit"></a>Bearbeiten  
Klicken Sie auf diese Option, um einen Datentyp in der Zuordnungsliste zu bearbeiten.  
  
##### <a name="remove"></a>Entfernen  
Klicken Sie auf diese Option, um die ausgewählte Zuordnung aus der Zuordnungsliste zu entfernen.  
  
##### <a name="reset-to-default"></a>Standard wiederherstellen  
Klicken Sie auf diese Option, um alle datentypzuordnungen auf die SSMA-Standardwerte zurückzusetzen.  
  
