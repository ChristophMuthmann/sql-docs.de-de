---
title: Microsoft Excel-Datentypen | Microsoft Docs
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
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5b18d5969cc2586fec45320af4a754a12276663d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel-Datentypen
Die folgende Tabelle zeigt, wie Microsoft Excel-Treiber-Datentypen in ODBC-SQL-Datentypen zugeordnet werden. Microsoft Excel-Treibers weist dieser Datentypen zu Spalten in Microsoft Excel-Tabellen basierend auf den Daten in der Spalte.  
  
|Microsoft Excel-Datentyp|ODBC-Datentyp|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LOGISCHE|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** gibt ODBC SQL-Datentypen. Alle Konvertierungen in Anhang D der *ODBC Programmer's Reference* werden für die ODBC-SQL-Datentypen, die weiter oben in diesem Thema aufgeführten unterstützt.  
  
 Die folgende Tabelle zeigt die Einschränkungen für Microsoft Excel-Datentypen.  
  
|Datentyp|Description|  
|---------------|-----------------|  
|Verschlüsselte Daten|Der Microsoft Excel-Treiber kann nicht auf verschlüsselte Daten gelesen.|  
|Fehlerzeichenfolgen|Der Microsoft Excel-Treiber kann keine Zeichenfolge für die Microsoft Excel-Fehlerwerte zurück (#n!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME?, und #NULL!), sondern stattdessen eine NULL zurück.|  
|LOGISCHE|Der Wert in eine logische Spalte wird in eine SQL_C_CHAR-Puffer als 0 oder 1 zurückgegeben.|  
|NUMBER|Wenn eine Spalte mit ganzen Zahlen erstellt wird, Zahlen, die für den Integer-Datentyp zu groß sind, können eingegeben werden, und Daten, die nicht ganzzahlige Werte eingefügt werden können, mit dem Ergebnis, dass die Spalte in SQL_DOUBLE konvertiert werden kann.|  
|TEXT|Wenn die Zeilen einer Spalte mehr als ein Microsoft Excel-Datentyp enthalten, mit ODBC Microsoft Excel-Treibers die Spalte den SQL_VARCHAR-Datentyp zugewiesen. Es wird eine Ausnahme: Wenn die Spalte nur zwei oder drei Datetime-Datentypen (DATE, TIME und DATETIME) enthält, weist ODBC Microsoft Excel-Treibers SQL_TIMESTAMP-Datentyp der Spalte.<br /><br /> Erstellen eine Textspalte mit 0 (null) oder nicht angegebene Länge gibt tatsächlich eine 255 Byte-Spalte.<br /><br /> Ein Zeichenfolgenliteral kann jedes ANSI-Zeichen (1-255 dezimal) enthalten. Verwenden Sie zwei aufeinander folgende einfache Anführungszeichen ("), um ein einfaches Anführungszeichen (') darzustellen.<br /><br /> Einfügen von NULL in eine Spalte mit einem anderen Datentyp als SQL_VARCHAR führt dazu, dass den Datentyp der Spalte, die in SQL_VARCHAR zu ändern.|  
  
 Weitere Einschränkungen für Datentypen finden Sie in [Datentyp Einschränkungen](../../odbc/microsoft/data-type-limitations.md).
