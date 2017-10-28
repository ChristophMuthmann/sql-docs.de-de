---
title: Projekteinstellungen (Zuordnung) (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4cefe036943dd986cbc6b1cd9cab2b44c9e0f9fd
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-type-mapping-oracletosql"></a>Projekteinstellungen (Zuordnung) (OracleToSQL)
Die Seite "Type Mapping", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA Oracle-Datentypen in konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen.  
  
Die Seite "Type Mapping" steht in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Zum Angeben von Einstellungen für alle zukünftigen SSMA-Projekte, auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste, und klicken Sie dann auf **Type Mapping** unten im linken Bereich.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, und klicken Sie dann auf **Type Mapping** unten im linken Bereich.  
  
Verwenden Sie zum Angeben von Einstellungen für das aktuelle Objekt oder eine Klasse von Objekten der **Type Mapping** Registerkarte im primären SSMA-Fenster.  
  
## <a name="options"></a>enthalten  
Die folgende Tabelle zeigt die **Type Mapping** Registerkarte Optionen:  
  
**Quelltyp**  
Der zugeordnete Oracle-Datentyp.  
  
**Zieltyp**  
Das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentyp für den angegebenen Datentyp von Oracle.  
  
Finden Sie in den Tabellen im nächsten Abschnitt für den standardmäßigen SSMA für Oracle-datentypzuordnungen.  
  
**Hinzufügen**  
Klicken Sie auf diese Option, um einen Datentyp der Zuordnungsliste hinzuzufügen.  
  
**Bearbeiten**  
Klicken Sie auf diese Option, um den ausgewählten Datentyp in der Zuordnungsliste zu bearbeiten.  
  
**Entfernen**  
Klicken Sie auf diese Option, um die ausgewählte Zuordnung aus der Zuordnungsliste zu entfernen.  
  
**Standard wiederherstellen**  
Klicken Sie auf diese Option, um die Liste ' datentypzuordnung ' auf die SSMA-Standardwerte zurückzusetzen.  
  
## <a name="default-type-mappings"></a>Standard-Datentypzuordnungen  
In SSMA für Oracle können Sie benutzerdefinierte datentypzuordnungen für Argumente, die Spalten, die lokalen Variablen und die Rückgabewerte festlegen. Die standardzuordnung für Argumente und Rückgabetypen ist nahezu identisch.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Standard-Argumenttyp und Typzuordnung Wert zurückgeben  
Die folgende Tabelle enthält die standardmäßige datentypzuordnung für Argumente und Rückgabewerte.  
  
|Oracle-Datentyp|Standard [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|BINARY_DOUBLE|"float" [53]|  
|BINARY_FLOAT|"float" [53]|  
|binary_integer|int|  
|Blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|CLOB|varchar(max)|  
|Datum|datetime2 [0]|  
|dec|DEC [38] [0]|  
|Decimal|"float" [53]|  
|mit doppelter Genauigkeit|"float" [53]|  
|float|"float" [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [\*... 8000]<sup>*</sup>|Varbinary [*]|  
|Long raw [8001..\*]<sup>*</sup>|varbinary(max)|  
|National char|nvarchar(max)|  
|National Char varying|nvarchar(max)|  
|nationale Zeichensätze|nvarchar(max)|  
|nationale Zeichensätze varying<sup>**</sup>|nvarchar(max)|  
|nationale Zeichensätze varying<sup>*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|number|"float" [53]|  
|numeric|"float" [53]|  
|NVARCHAR2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|"float" [53]|  
|ROWID|uniqueidentifier|  
|signtype|smallint|  
|smallint|smallint|  
|Zeichenfolge|varchar(max)|  
|timestamp|datetime2|  
|Zeitstempel mit der lokalen Zeitzone|datetimeoffset|  
|Zeitstempel mit Zeitzone|datetimeoffset|  
|UROWID|uniqueidentifier|  
|varchar|varchar(max)|  
|VARCHAR2|varchar(max)|  
|XmlType|xml|  
  
<sup>*</sup>Gilt für Typ wertezuordnung nur zurückgeben.  
  
<sup>**</sup>Gilt für das Argument Typ nur zuordnen.  
  
### <a name="default-column-type-mapping"></a>Standardtypmapping Spalte  
Die folgende Tabelle enthält die Standard-Typzuordnung für Spalten.  
  
|Oracle-Datentyp|Standard [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|BINARY_DOUBLE|"float" [53]|  
|BINARY_FLOAT|"float" [53]|  
|Blob|varbinary(max)|  
|char|char|  
|Char varying [*.. \*]|Varchar [*]|  
|Char [*.. \*]|Char [*]|  
|character|char|  
|unterschiedliche Zeichen [*.. \*]|Varchar [*]|  
|Zeichen [*.. \*]|Char [*]|  
|CLOB|varchar(max)|  
|Datum|datetime2 [0]|  
|dec|DEC [38] [0]|  
|DEC [*.. \*]|DEC [*] [0]|  
|DEC [*.. \*][\*.. \*]|dec[*][\*]|  
|Decimal|Dezimal [38] [0]|  
|Dezimal [*.. \*]|Dezimal [*] [0]|  
|Dezimal [*.. \*][\*.. \*]|Dezimal [*] [\*]|  
|mit doppelter Genauigkeit|"float" [53]|  
|float|"float" [53]|  
|"float" [*.. 53]|"float" [*]|  
|"float" [54.. *]|"float" [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*.. 8000]|Varbinary [*]|  
|Long raw [8001.. *]|varbinary(max)|  
|lange varchar|varchar(max)|  
|lange [*.. 8000]|Varchar [*]|  
|lange [8001.. *]|varchar(max)|  
|National char|nchar|  
|National Char varying [*.. \*]|Nvarchar [*]|  
|National Char [*.. \*]|NCHAR [*]|  
|nationale Zeichensätze|nchar|  
|nationale Zeichensätze varying [*.. \*]|Nvarchar [*]|  
|nationale Zeichensätze [*.. \*]|NCHAR [*]|  
|nchar|nchar|  
|NCHAR [*]|NCHAR [*]|  
|NCLOB|nvarchar(max)|  
|number|"float" [53]|  
|Anzahl [*.. \*]|numerische [*]|  
|Anzahl [*.. \*][\*.. \*]|numerische [*] [\*]|  
|numeric|numeric|  
|numerische [*.. \*]|numerische [*]|  
|numerische [*.. \*][\*.. \*]|numerische [*] [\*]|  
|NVARCHAR2 [*.. \*]|Nvarchar [*]|  
|Rohdaten [*.. \*]|Varbinary [*]|  
|real|"float" [53]|  
|ROWID|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|Zeitstempel mit der lokalen Zeitzone|datetimeoffset|  
|Zeitstempel mit der lokalen Zeitzone [*.. \*]|"DateTimeOffset" [*]|  
|Zeitstempel mit Zeitzone|datetimeoffset|  
|Zeitstempel mit Zeitzone [*.. \*]|"DateTimeOffset" [*]|  
|Zeitstempel [*.. \*]|datetime2 [*]|  
|UROWID|uniqueidentifier|  
|UROWID [*.. \*]|uniqueidentifier|  
|Varchar [*.. \*]|Varchar [*]|  
|VARCHAR2 [*.. \*]|Varchar [*]|  
|XmlType|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Standardtypmapping lokale Variablen  
Die folgende Tabelle enthält die Standard-Typzuordnung für lokale Variablen.  
  
|Oracle-Datentyp|Standard [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|BINARY_DOUBLE|"float" [53]|  
|BINARY_FLOAT|"float" [53]|  
|binary_interger|int|  
|BLOB|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|Char varying [*.. 8000]|Varchar [*]|  
|Char varying [8001.. *]|varchar(max)|  
|Char [*.. 8000]|Char [*]|  
|Char [8001.. *]|varchar(max)|  
|Zeichen|char|  
|unterschiedliche Zeichen [*.. 8000]|Varchar [*]|  
|unterschiedliche Zeichen [8001.. *]|varchar(max)|  
|Zeichen [*.. 8000]|Char [*]|  
|Zeichen [8001.. *]|varchar(max)|  
|CLOB|varchar(max)|  
|Datum|datetime2 [0]|  
|dec|DEC [38] [0]|  
|DEC [*.. \*]|DEC [*] [0]|  
|DEC [*.. \*][\*.. \*]|dec[*][\*]|  
|Decimal|Dezimal [38] [0]|  
|Dezimal [*.. \*]|Dezimal [*] [0]|  
|Dezimal [*.. \*][\*.. \*]|Dezimal [*] [\*]|  
|mit doppelter Genauigkeit|"float" [53]|  
|Float|"float" [53]|  
|"float" [*.. 53]|"float" [*]|  
|"float" [54.. *]|"float" [53]|  
|int|int|  
|Integer|int|  
|ganze Zahl [*.. \*]|numerische [*] [0]|  
|Long|varchar(max)|  
|Long raw|varbinary(max)|  
|Long raw [*.. 8000]|Varbinary [*]|  
|Long raw [8001.. *]|varbinary(max)|  
|National char|nchar|  
|National Char varying [*.. 4000]|Nvarchar [*]|  
|National Char varying [4001.. *]|nvarchar(max)|  
|National Char [*.. 4000]|NCHAR [*]|  
|National Char [4001.. *]|nvarchar(max)|  
|nationale Zeichensätze|nchar|  
|nationale Zeichensätze [*.. 4000]|Nvarchar [*]|  
|nationale Zeichensätze [4001.. *]|nvarchar(max)|  
|nationale Zeichensätze varying [*.. 4000]|Nvarchar [*]|  
|nationale Zeichensätze varying [4001.. *]|nvarchar(max)|  
|Nchar|nchar|  
|NCHAR [*.. 4000]|NCHAR [*]|  
|NCHAR [4001.. *]|nvarchar(max)|  
|NCHAR varying [*.. 4000]|Nvarchar [*]|  
|NCHAR varying [4001.. *]|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|Number|"float" [53]|  
|Anzahl [*.. \*]|numerische [*]|  
|Anzahl [*.. \*][\*.. \*]|numerische [*] [\*]|  
|Numerisch|numerische [38] [0]|  
|numerische [*.. \*]|numerische [*]|  
|numerische [*.. \*][\*.. \*]|numerische [*] [\*]|  
|NVARCHAR2 [*.. 4000]|Nvarchar [*]|  
|NVARCHAR2 [4001.. *]|nvarchar(max)|  
|pls_integer|int|  
|Rohdaten [*.. 8000]|Varbinary [*]|  
|Rohdaten [8001.. *]|varbinary(max)|  
|Real|"float" [53]|  
|ROWID|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|Zeichenfolge [*.. 8000]|Varchar [*]|  
|Zeichenfolge [8001.. *]|varchar(max)|  
|timestamp|datetime2|  
|Zeitstempel mit der lokalen Zeitzone|datetimeoffset|  
|Zeitstempel mit Zeitzone|datetimeoffset|  
|Zeitstempel mit der lokalen Zeitzone [*.. \*]|"DateTimeOffset" [*]|  
|Zeitstempel mit Zeitzone [*.. \*]|"DateTimeOffset" [*]|  
|Zeitstempel [*.. \*]|datetime2 [*]|  
|UROWID|uniqueidentifier|  
|UROWID [*.. \*]|uniqueidentifier|  
|Varchar [*.. 8000]|Varchar [*]|  
|Varchar [8001.. *]|varchar(max)|  
|VARCHAR2 [*.. 8000]|Varchar [*]|  
|VARCHAR2 [8001.. *]|varcha(max)|  
|XmlType|xml|  
  
## <a name="see-also"></a>Siehe auch  
[Referenz zur Benutzeroberfläche &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  

