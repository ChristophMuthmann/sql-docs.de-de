---
title: Datentyp Einschränkungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 309a539cc0f5758fd521e408e64f7155bc9ab9f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-limitations"></a>Data Type-Einschränkungen
Microsoft ODBC-Desktop-Datenbanktreiber festlegen, die folgenden Einschränkungen für Datentypen:  
  
|Datentyp|Description|  
|---------------|-----------------|  
|Alle Datentypen|Fehler bei der Konvertierung von Typ kommen die betreffende Spalte auf NULL festgelegt wird.|  
|BINARY|Erstellen eine leere BINÄRE Spalte gibt tatsächlich eine BINÄRE 255 Byte-Spalte zurück.|  
|DATE|Der DATE-Datentyp kann nicht auf einen anderen Datentyp (oder selbst) von der CONVERT-Funktion konvertiert werden.|  
|DECIMAL (genau numerisch)|Nicht unterstützt.|  
|Gleitkomma-Datentypen|Die Anzahl der Dezimalstellen in eine Gleitkommazahl kann durch das Zahlenformat, legen Sie im Abschnitt der Windows-Systemsteuerung internationale eingeschränkt werden.|  
|NUMERIC|Unterstützt die maximale Genauigkeit und Dezimalstellen 28.|  
|TIMESTAMP|Der TIMESTAMP-Datentyp kann nicht auf sich selbst von der CONVERT-Funktion konvertiert werden.|  
|TINYINT|"Tinyint" sind immer ohne Vorzeichen.|  
|Mit der Länge NULL-Zeichenfolgen|Wenn eine dBASE, Microsoft Excel, Paradox oder Textdriver verwendet wird, fügt eine Zeichenfolge der Länge 0 (null) in eine Spalte eingefügt. tatsächlich ein NULL-Wert stattdessen.|
