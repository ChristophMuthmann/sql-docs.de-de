---
title: Tabelle Name Einschränkungen | Microsoft Docs
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
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ffba1295cf16c48402987165e90c61bc9c5cc65
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="table-name-limitations"></a>Einschränkungen der Tabelle von Clientnamen
Tabellennamen können keine gültigen Zeichen (z. B. Leerzeichen) enthalten. Wenn Tabellennamen alle Zeichen außer Buchstaben, Zahlen und Unterstriche enthalten, muss der Namen getrennt werden, indem Sie es in Back Anführungszeichen (') einschließen.  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, und ein Tabellennamen wird nicht durch einen Datenbankverweis qualifiziert, wird die Standarddatenbank impliziert. Wenn ein Name in Microsoft Excel umfasst den "!" Zeichen ist, wird es automatisch übersetzt werden, die "$"-Zeichens stattdessen.  
  
 Den Namen der Microsoft Excel-Tabelle, die verweist \<Filename > wird für Microsoft Excel 3.0 und 4.0-Dateien unterstützt. Den Namen der Microsoft Excel-Tabelle, die verweist \<Arbeitsmappe-Name > ist für Microsoft Excel 5.0, 7.0 oder 97-Dateien unterstützt.  
  
 Wenn der Treiber dBASE verwendet wird, werden mit einem ASCII-Wert, der größer als 127 Zeichen in Unterstriche konvertiert.  
  
 Wenn der Microsoft Access-Treiber verwendet wird, ist der Tabellenname maximal 64 Zeichen umfassen.  
  
 Wenn dBASE, Microsoft Excel 3.0 oder 4.0, Paradox oder Text-Treiber verwendet wird, sollte speziellen MS-DOS-Schlüsselwörter CON "," AUX "," LPT1 "und" LPT2 nicht als Tabellennamen verwendet werden.
