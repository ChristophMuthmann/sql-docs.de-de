---
title: Literal-Präfixe und Suffixe | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d1d836c086747cba5b42b0db5a1919575afcfaa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="literal-prefixes-and-suffixes"></a>Literal-Präfixe und Suffixe
In einer SQL­Anweisung eine *literal* eine zeichendarstellung der einen Datenwert ist. In der folgenden Anweisung werden ABC, FFFF und 10 Literale:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literale für einige Datentypen erfordern besondere Präfixe und Suffixe an. Im vorherigen Beispiel der Zeichenliterale (ABC) ist ein einfaches Anführungszeichen (') als ein Präfix und Suffix erforderlich, die binäre Literal (FFFF) erfordert die Zeichen 0 X als Präfix und den Integer-literal (10) nicht benötigen ein Präfix oder suffix.  
  
 Für alle Datentypen außer Date, Time und Zeitstempel, sollten interoperable Anwendungen verwenden Sie die Werte zurückgegeben, die in den LITERAL_PREFIX-Zeichen und LITERAL_SUFFIX Spalten im Resultset erstellt, indem **SQLGetTypeInfo**. Datum, Uhrzeit, Timestamp und Datetime-Intervall-Literale sollten interoperable Anwendungen ausführen können die Escapesequenzen, die im vorherigen Abschnitt erläutert verwenden.
