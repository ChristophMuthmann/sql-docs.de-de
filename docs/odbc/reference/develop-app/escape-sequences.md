---
title: Escape-Zeichensequenzen | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9bb389cba92f45373e7fc693c9c4477d50a702a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="escape-sequences"></a>Escapesequenzen
ODBC definiert Escapesequenzen, die mit standard-Grammatik für Datum, Uhrzeit, Timestamp und Datetime-Intervall-literalen Aufrufe von Skalarfunktionen, **wie** Prädikat-Escape-Zeichen, äußere Joins und Prozeduraufrufe. Interoperable Anwendungen ausführen können, sollten diese Sequenzen möglichst verwenden.  
  
 Um festzustellen, ob ein Treiber die Escapesequenzen für Datum, Uhrzeit, Timestamp- oder Datetime-Intervall-Literale unterstützt, eine Anwendung ruft **SQLGetTypeInfo**. Wenn die Datenquelle ein Datum, Uhrzeit, Timestamp- oder Intervall-Datentyp "DateTime" unterstützt, muss es auch die entsprechende Escapesequenz unterstützen. Um zu bestimmen, ob die Escape-Sequenzen unterstützt werden, eine Anwendung ruft **SQLGetInfo**.  
  
 Weitere Informationen finden Sie unter [Escapesequenzen in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)weiter unten in diesem Abschnitt.
