---
title: Microsoft Access-Datentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: bee1801eb581272762b2f80d25eeb64d0220a256
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-access-data-types"></a>Microsoft Access-Datentypen
Die folgende Tabelle zeigt die Microsoft Access-Datentypen, die Datentypen, die zum Erstellen von Tabellen verwendet und die ODBC-SQL-Datentypen.  
  
|Microsoft Access-Datentyp|-Datentyp (CREATETABLE)|ODBC-SQL-Datentyp|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|LEISTUNGSINDIKATOR|LEISTUNGSINDIKATOR|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATUM/UHRZEIT|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|LANGE BINÄRE|LONGBINARY|SQL_LONGVARBINARY|  
|LANGER TEXT|LONGTEXT|SQL_WLONGVARCHAR FÜR SQL_LONGVARCHAR [2] [3]|  
|MEMO|LONGTEXT|SQL_WLONGVARCHAR FÜR SQL_LONGVARCHAR [2] [3]|  
|Anzahl (Feldgröße = SINGLE)|EINZELNE|SQL_REAL|  
|Anzahl (Feldgröße = DOUBLE)|DOUBLE|SQL_DOUBLE|  
|Anzahl (Feldgröße = BYTE)|BYTE OHNE VORZEICHEN|SQL_TINYINT|  
|Anzahl (Feldgröße = INTEGER)|KURZE|SQL_SMALLINT|  
|Anzahl (Feldgröße = LONG Integer-Wert)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|[1]-SQL_VARCHAR, SQL_WVARCHAR [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] nur Access 4.0-Anwendungen. Maximale Länge von 4.000 Byte. Verhalten LONGBINARY ähnelt.  
  
 ' [2] ' nur ANSI-Anwendungen.  
  
 [3] nur für Unicode- und Access 4.0-Anwendungen.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** gibt ODBC-Datentypen. Es wird nicht alle Microsoft Access-Datentypen zurückgegeben, wenn mehr als eine Microsoft Access-Typ in den gleichen ODBC SQL-Datentyp zugeordnet ist. Alle Konvertierungen in Anhang D der *ODBC Programmer's Reference* werden für die SQL-Datentypen, die in der vorherigen Tabelle aufgeführten unterstützt.  
  
 Die folgende Tabelle zeigt die Einschränkungen für Microsoft Access-Datentypen.  
  
|Datentyp|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY und VARCHAR|Erstellen einer BINARY, VARBINARY und VARCHAR-Spalte 0 (null) oder nicht angegebene Länge gibt tatsächlich eine 510-Byte-Spalte.|  
|BYTE|Obwohl ein Feld für die Microsoft Access Zahl mit einem BYTE gleich Feldgröße nicht signiert ist, kann eine negative Zahl in das Feld eingefügt werden, wenn der Microsoft Access-Treiber verwendet.|  
|LONGVARCHAR, CHAR und VARCHAR|Ein Zeichenfolgenliteral kann jedes ANSI-Zeichen (1-255 dezimal) enthalten. Verwenden Sie zwei aufeinander folgende einfache Anführungszeichen ("), um ein einfaches Anführungszeichen (') darzustellen.<br /><br /> Verfahren sollte verwendet werden, um Zeichendaten zu übergeben, bei Verwendung von Sonderzeichen in einem Zeichen-Datentypspalte.|  
|DATE|Datumswerte müssen werden gemäß der kanonischen ODBC-Datumsformat getrennt oder durch das Trennzeichen "DateTime" ("#") als Trennzeichen. Andernfalls wird Microsoft Access als einem arithmetischen Ausdruck den Wert behandelt und löst keine Warnung oder einen Fehler.<br /><br /> Z. B. das Datum "5. März 1996" muss, als dargestellt werden {d ' 1996-03-05 "} oder #03/05/&#1996; andernfalls, wenn nur 03/05/1993 gesendet wird, wird Microsoft Access dies als 3 geteilt durch 5 geteilt durch 1996 ausgewertet. Dieser Wert aufgerundet wird auf die ganze Zahl 0, und da 0 (null) Tag 1899-12-31 zugeordnet wird, ist dies das Datum verwendet.<br /><br /> Einen senkrechten Strich (&#124;) kann nicht in einen Date-Wert verwendet werden, auch wenn es wieder in Anführungszeichen eingeschlossen.|  
|GUID|Beschränkt auf Microsoft Access 4.0 Datentyp.|  
|NUMERIC|Beschränkt auf Microsoft Access 4.0 Datentyp.|  
  
 Weitere Einschränkungen für Datentypen finden Sie in [Datentyp Einschränkungen](../../odbc/microsoft/data-type-limitations.md).
