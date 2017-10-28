---
title: Zuordnen von MySQL und SQL Server-Zeichen festgelegt (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1145e4168e41f2014b95e7315a17dd00d764c386
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Zuordnen von MySQL und SQL Server-Zeichen (MySQLToSQL) festlegen
Zeichensatz (Zeichensatz) kann für MySQL-Unicodezeichen-Datentypen, Ausdrücke und Literale angegeben werden.  
  
## <a name="charset-mapping"></a>CharSet-Zuordnung  
CharSet-Zuordnung für jede MySQL-Zeichensatz definiert und während der datentypkonvertierung Zeichen verwendet. Es gibt an, wie Zeichenfolgen-Datentypen für einen bestimmten Zeichensatz zu konvertieren:  
  
-   National SQL Server-Zeichen-Datentypen (NCHAR/NVARCHAR) oder  
  
-   Reguläre SQL Server-Zeichen-Datentypen (CHAR/VARCHAR)  
  
1.  **National** Ziel Datenbank Unicodezeichen-Datentypen sind:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **reguläre** Ziel Datenbank Unicodezeichen-Datentypen sind:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  Typzuordnung lässt nur eine Zuordnung zu **national** Zeichendatentypen. Nachdem gemäß Typmapping MySQL Zeichendatentyp konvertiert wurde, wird Charset-Zuordnung angewendet.  
  
> [!NOTE]  
> CharSet-Zuordnung kann auf jeder Knotenebene des Objekt-Explorers Metadaten definiert werden und alle Zeichensätze MySQL auslesen darstellen.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Zeichensatz auf unterschiedlichen Knotenebenen zuordnen  
Zuordnen von CharSet variiert auf unterschiedlichen Knotenebenen, nämlich:  
  
1.  Auf der Ebene des Schemastammknotens Metadaten  
  
2.  Für Datenbank "," Category "und" Knoten Objektebene  
  
> [!NOTE]  
> Die Registerkarte ausgewählt wird, für die Bearbeitung der Charset-Zuordnung enthält drei Schaltflächen aus, unabhängig von der Zuordnung für die unterschiedlichen Knotenebenen.  
>   
> Die Überladungen sind:  
>   
> 1.  **Gelten:** wendet Änderungen durch den Benutzer nur aktiviert, wenn Charset-Zuordnung bearbeitet und noch nicht gespeichert ist.  
> 2.  **"Abbrechen":** Änderungen, die vom Benutzer abgebrochen. Die Schaltfläche ruft aktiviert, wenn Charset-Zuordnung wird bearbeitet, aber nicht gespeichert.  
> 3.  **Standard wiederherstellen:** setzt alle Zuordnungen auf Standardwerte zurück.  
  
1.  **Auf Metadaten Ebene des Schemastammknotens:** Charset Zuordnungsraster enthält Charset-Raster mit einer separaten Spalte für jeden Zeichensatz. Die Spalten des Rasters sind:  
  
    1.  Die erste Spalte des Rasters mit dem Namen **Charset Namen** Charset-Namen enthält.  
  
    2.  Das zweite Argument, das mit dem Namen **Charset Beschreibung** Charset-Beschreibung enthält.  
  
    3.  Die dritte Spalte mit dem Titel, **Charset-Zieltyp** enthält Einstellungen für die identitätszuordnung für bestimmte Zeichensatz. Werte für diese Spalte sind:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > Die Standardwerte für einen bestimmten Charset haben das Präfix "(Standard)" nach CHAR/VARCHAR oder NCHAR/NVARCHAR.  
  
    Die Charset-Zuordnung zwischen MySQL-Datenbank und die Zieldatenbank auf Ebene des Schemastammknotens Metadaten ist unten angegeben:  
  
    ||||  
    |-|-|-|  
    |**CharSet-Name**|**CharSet-Beschreibung**|**Charset Zieltyp (Standard)**|  
    |Big5|Chinesisch (traditionell) Big5|NCHAR/NVARCHAR (Standard)|  
    |dec8|DEC West Europäischen|CHAR/VARCHAR (Standard)|  
    |cp850|DOS-West Europäischen|CHAR/VARCHAR (Standard)|  
    |hp8|HP West Europäischen|CHAR/VARCHAR (Standard)|  
    |koi8r|KOI8-r Relcom Russisch|CHAR/VARCHAR (Standard)|  
    |Latin 1|cp1252 West Europäischen|CHAR/VARCHAR (Standard)|  
    |Lateinisch 2|ISO 8859-2 Mitteleuropa|CHAR/VARCHAR (Standard)|  
    |swe7|7-Bit-Schwedisch|CHAR/VARCHAR (Standard)|  
    |ASCII|US-ASCII|CHAR/VARCHAR (Standard)|  
    |ujis|EUC-JP Japanisch|NCHAR/NVARCHAR (Standard)|  
    |SJIS|Shift-JIS Japanisch|NCHAR/NVARCHAR (Standard)|  
    |Hebräisch|ISO 8859-8 Hebrew|CHAR/VARCHAR (Standard)|  
    |tis620|Thailändisch TIS620|CHAR/VARCHAR (Standard)|  
    |eucKR|EUC-KR Koreanisch|NCHAR/NVARCHAR (Standard)|  
    |koi8u|KOI8-u Ukrainisch|CHAR/VARCHAR (Standard)|  
    |GB2312|GB2312 Chinesisch (vereinfacht)|NCHAR/NVARCHAR (Standard)|  
    |Griechisch|ISO 8859-7 Greek|CHAR/VARCHAR (Standard)|  
    |CP 1250|Windows-Mitteleuropäisch|CHAR/VARCHAR (Standard)|  
    |GBK|GBK, vereinfachtes Chinesisch|NCHAR/NVARCHAR (Standard)|  
    |Latin5|ISO 8859-9 Turkish|CHAR/VARCHAR (Standard)|  
    |armscii8|ARMSCII 8 Armenisch|CHAR/VARCHAR (Standard)|  
    |UTF8|Unicode UTF-8|NCHAR/NVARCHAR (Standard)|  
    |ucs2|Unicode UCS-2|NCHAR/NVARCHAR (Standard)|  
    |cp866|DOS Russisch|CHAR/VARCHAR (Standard)|  
    |keybcs2|DOS Kamenicky Tschechisch-Slowakisch|CHAR/VARCHAR (Standard)|  
    |macce|Mitteleuropäisch Mac|CHAR/VARCHAR (Standard)|  
    |MacRoman|Mac-West-Europäischen|CHAR/VARCHAR (Standard)|  
    |cp852|DOS-Mitte Europäischen|CHAR/VARCHAR (Standard)|  
    |Latin7|ISO 8859-13-Baltisch|CHAR/VARCHAR (Standard)|  
    |CP 1251|Windows-Kyrillisch|CHAR/VARCHAR (Standard)|  
    |CP 1256|Windows-Arabisch|CHAR/VARCHAR (Standard)|  
    |CP 1257|Windows-Baltisch|CHAR/VARCHAR (Standard)|  
    |binary|Binäre Pseudo-Zeichensatz|CHAR/VARCHAR (Standard)|  
    |geostd8|Georgisch GEOSTD8|CHAR/VARCHAR (Standard)|  
    |cp932|SJIS für Japanisch für Windows|NCHAR/NVARCHAR (Standard)|  
    |eucjpms|UJIS für Japanisch für Windows|NCHAR/NVARCHAR (Standard)|  
  
2.  **In der Datenbank, Kategorie oder Objekt Knotenebenen:** auf der Ebene des Datenbank-, Kategorie oder Objektknoten enthält Charset Zuordnungsraster dieselben Zeilen wie auf der Ebene des schemastammknotens Metadaten, begrenzt.:  
  
    1.  Die erste Spalte des Rasters mit dem Titel, **Zeichennamen festgelegt** Charset-Namen enthält.  
  
    2.  Die zweite Spalte mit dem Titel, **Zeichen festgelegt Beschreibung** Charset-Beschreibung enthält.  
  
    3.  Der einzige Unterschied ist die Werte in der dritten Spalte des Rasters. Die dritte Spalte mit dem Titel, **Zieldatentyp** enthält Einstellungen für die identitätszuordnung für bestimmte Zeichensatz. Die Werte für die Spalte sind:  
  
        -   Geerbte (CHAR/VARCHAR oder NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   In der Charset-Zuordnung zwischen MySQL-Datenbank und die Zieldatenbank auf Datenbank-, Kategorie und Objektebenen für die Knoten, die Standardwerte für einen bestimmten Zeichensatz für jede Ebene als Stammverzeichnis für die Spalte **Zieldatentyp** sollte "vererbt".  
> -   Im Raster, den Wert **geerbte** ist entweder mit dem Suffix '(CHAR/VARCHAR) "oder '(NCHAR/NVARCHAR)" je nachdem, welcher Wert von dieser bestimmten Charset vom übergeordneten Element geerbt wurde.  
  

