---
title: "Tabelle Name Einschränkungen | Microsoft Docs"
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
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 690b6242b9e8d38b6a1f26ddbd823215030e2b15
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="table-name-limitations"></a>Einschränkungen der Tabelle von Clientnamen
Tabellennamen können keine gültigen Zeichen (z. B. Leerzeichen) enthalten. Wenn Tabellennamen alle Zeichen außer Buchstaben, Zahlen und Unterstriche enthalten, muss der Namen getrennt werden, indem Sie es in Back Anführungszeichen (') einschließen.  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, und ein Tabellennamen wird nicht durch einen Datenbankverweis qualifiziert, wird die Standarddatenbank impliziert. Wenn ein Name in Microsoft Excel umfasst den "!" Zeichen ist, wird es automatisch übersetzt werden, die "$"-Zeichens stattdessen.  
  
 Den Namen der Microsoft Excel-Tabelle, die verweist \<Filename > wird für Microsoft Excel 3.0 und 4.0-Dateien unterstützt. Den Namen der Microsoft Excel-Tabelle, die verweist \<Arbeitsmappe-Name > ist für Microsoft Excel 5.0, 7.0 oder 97-Dateien unterstützt.  
  
 Wenn der Treiber dBASE verwendet wird, werden mit einem ASCII-Wert, der größer als 127 Zeichen in Unterstriche konvertiert.  
  
 Wenn der Microsoft Access-Treiber verwendet wird, ist der Tabellenname maximal 64 Zeichen umfassen.  
  
 Wenn dBASE, Microsoft Excel 3.0 oder 4.0, Paradox oder Text-Treiber verwendet wird, sollte speziellen MS-DOS-Schlüsselwörter CON "," AUX "," LPT1 "und" LPT2 nicht als Tabellennamen verwendet werden.

