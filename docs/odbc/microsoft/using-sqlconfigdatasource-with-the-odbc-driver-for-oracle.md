---
title: "Der ODBC-Treiber für Oracle SQLConfigDatasource mit | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa32db53ef43da7f01200dcf057f9855a4f5707e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Verwenden von SQLConfigDatasource mit dem ODBC-Treiber für Oracle
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Die folgende Tabelle enthält gültige **SQLConfigDatasource** Einstellungen für den Microsoft ODBC-Treiber für Oracle, Version 1.0 (Msorcl10.dll) und der Microsoft ODBC-Treiber für Oracle, Version 2.0 (Msorcl32.dll).  
  
> [!NOTE]  
>  Der Msorcl10.dll-Treiber (Version 1.0) unterstützt alle Einstellungen, mit Ausnahme von **Server**. Der Treiber Msorcl32.dll (Version 2.0 und höher) unterstützt alle Einstellungen.  
  
 Einige Einstellungen werden vom Treiber ignoriert jedoch akzeptiert werden, indem **SQLConfigDatasource**. Diese Einstellungen in der ODBC-Verbindungszeichenfolge einschließlich ist die einzige Möglichkeit, die sie zur Laufzeit akzeptiert werden. Eine ignorierte Einstellung wird nicht in der Registrierung gespeichert werden beim **SQLConfigDatasource** Erstellen der Datenquelle.  
  
 In der folgenden Tabelle *eine/N* bedeutet, dass jede gültige alphanumerische Zeichenfolge bis zu die maximal zulässige Länge. *Max. Len* (maximale Länge) ist die maximale zulässige Zeichenfolgenlänge von der Einstellung, einschließlich das zeichenfolgenabschlusszeichen Zeichen akzeptiert.  
  
|Einstellung|Max. Länge|Standardwert|Gültige Werte|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Minimale Fetchpuffer Größe bis 65535 bytes|  
|CatalogCap|2|1|0 oder 1|Bei 1 werden nonquoted Bezeichner in Großbuchstaben umwandeln im Katalog Funktionen.|  
|ConnectString|128|""|EINE/N|Verbindungszeichenfolge. Erforderliche Methode mit dem Treiber Msorcl10.dll des Servernamens.|  
|Description|256|""|EINE/N|Beschreibung|  
|DSN|33|""|EINE/N|Datenquellenname.|  
|GuessTheColDef|4|0|EINE/N|Gibt einen Wert ungleich NULL für Spalten ohne die Dezimalstellenanzahl Oracle definiert.|  
|NumberFloat|2|""|0 oder 1|Bei 0 werden als SQL_FLOAT FLOAT-Spalten behandelt. Bei 1 werden FLOAT-Spalten als SQL_DOUBLE behandelt.|  
|PWD|30|""|EINE/N|Das Kennwort.|  
|RDOSupport|2|""|0 oder 1|Ermöglicht das RDO Oracle Prozeduren aufrufen.|  
|Hinweise|2|0|0 oder 1|Schließen Sie "Hinweise" in Katalogfunktionen.|  
|RowLimit|4|""|0 bis 99|Maximale Anzahl der von einer SELECT-Anweisung zurückgegebenen Zeilen. Eine Zeichenfolge der Länge 0 (null) gibt an, dass keine Beschränkung angewendet wird.|  
|Server|128|""|EINE/N|Der Name der Oracle-Servers.|  
|SynonymColumns|2|1|0 oder 1|Schließen Sie Synonyme in SQLColumns.|  
|SystemTable|2|""|0 oder 1|Bei 0 werden die Systemtabellen nicht angezeigt. Bei 1 werden Systemtabellen angezeigt.|  
|TranslationDLL|33|""|EINE/N|Translation-DLL-Namen.|  
|TranslationName|33|""|EINE/N|Name der Übersetzung.|  
|TranslationOption|33|""|EINE/N|Translation-Option.|  
|TxnCap|2|""|EINE/N|Die Transaktion kann. Bei 0, gibt der Treiber an, dass Transaktionen nicht unterstützt wird. Bei 1, meldet der Treiber an, dass es sich bei der Durchführung von Transaktionen kann.|  
|UID|30|""|EINE/N|Name des Benutzers.|
