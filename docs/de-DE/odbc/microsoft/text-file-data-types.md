---
title: Datei-Textdatentypen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 87707e3fe68c506d6774ffaa9aceb8ddc5a18223
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="text-file-data-types"></a>Text-Datei-Datentypen
In der folgenden Tabelle wird gezeigt, wie Text-Datentypen in ODBC-SQL-Datentypen zugeordnet werden. Beachten Sie, dass nicht alle ODBC-SQL-Datentypen von der Text der ODBC-Treiber unterstützt werden.  
  
|Text-Datentyp|ODBC-Datentyp|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|GLEITKOMMAZAHL|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** gibt ODBC-Datentypen. Alle Konvertierungen in Anhang D der *ODBC Programmer's Reference* werden für die SQL-Datentypen, die in der vorherigen Tabelle aufgeführten unterstützt.  
  
 Die folgende Tabelle zeigt die Einschränkungen für Datentypen Text.  
  
|Datentyp|Description|  
|---------------|-----------------|  
|CHAR|Erstellen eine CHAR-Spalte 0 (null) oder nicht angegebene Länge gibt tatsächlich eine 255-Bit-Spalte zurück.<br /><br /> In durch Trennzeichen getrennte Dateien eine CHAR-Spalte kann oder möglicherweise keine Anführungszeichen Trennzeichen am Anfang und Ende; in Dateien mit fester Länge werden doppelte Anführungszeichen als Trennzeichen nicht verwendet.|  
|DATETIME|MM-DD-YY (z. B. 01 – 17-92)<br /><br /> MMM-DD-YY (z. B. Januar-17-92)<br /><br /> DD-MMM-YY (z. B. 17 Jan. 92)<br /><br /> JJJJ-MM-TT (z. B. 1992-01-17)<br /><br /> JJJJ-MMM-TT (z. B. 1992-Jan-17)<br /><br /> Gemischte Datumstrennzeichen dürfen nicht innerhalb einer Tabelle.<br /><br /> Text-ISAM-Formate ein DATETIME-Feld in den Vereinigten Staaten oder Europäischen-Format je nach der internationalen Einstellung in der Windows-Systemsteuerung.|  
|GLEITKOMMAZAHL|Die maximale Breite enthält, die Anmeldung und ein Dezimaltrennzeichen. In Schema.ini wird die Breite folgendermaßen gekennzeichnet:<br /><br /> 14.083 ist FLOAT Breite 6<br /><br /> -14.083 ist FLOAT Breite 7<br /><br /> +14.083 ist FLOAT Breite 7<br /><br /> 14083. ist "float" Breite 6<br /><br /> ODBC gibt immer 8 für FLOAT-Spalten zurück.<br /><br /> FLOAT-Spalten können z. B. auch in der wissenschaftlichen Schreibweise sein:<br /><br /> -3.04E + 2 ist Float Breite 8<br /><br /> 25E4 ist Float Breite 4<br /><br /> **Hinweis** Decimal "und" wissenschaftliche Notation kann in einer Spalte nicht gemischt werden.<br /><br /> NULL-Werte werden durch eine leere mit Nullen aufgefüllten Zeichenfolge fester Länge Dateien dargestellt und in Dateien mit Trennzeichen ausgelassen.<br /><br /> Float-Daten können mit führenden Leerzeichen aufgefüllt werden.|  
|INTEGER|Gültige Werte für Spalten sind 32.767-32766.<br /><br /> In Schema.ini wird die Breite folgendermaßen gekennzeichnet:<br /><br /> 14083 ist INTEGER Breite 5<br /><br /> 0 ist die Breite 1 ganze Zahl<br /><br /> ODBC gibt immer 4 für Spalten zurück.<br /><br /> Die maximale Breite einschließt ein Vorzeichen. Die maximale Breite der Spalte mit ganzen Zahlen ist 11, obwohl die Breite aufgrund von Leerzeichen größer sein kann, die in Tabellen mit festem Format zulässig sind.|  
|LONGCHAR|Der theoretische Grenze für die Breite einer Spalte LONGCHAR entweder in eine feste Länge, oder durch Trennzeichen getrennten Tabelle kann 65500K. Text-ISAM ist wahrscheinlicher zuverlässige unterstützen bis zu 32 KB.|  
  
 Weitere Einschränkungen für Datentypen finden Sie in [Datentyp Einschränkungen](../../odbc/microsoft/data-type-limitations.md).
