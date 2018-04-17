---
title: Datentyp Einschränkungen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f7be82a89d81f887baf0ae6ef0fe7cd00e72c27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
