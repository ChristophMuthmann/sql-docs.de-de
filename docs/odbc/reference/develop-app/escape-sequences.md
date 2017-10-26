---
title: Escape-Zeichensequenzen | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c648549b41ff607ad34175475c6a2b75603625f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="escape-sequences"></a>Escapesequenzen
ODBC definiert Escapesequenzen, die mit standard-Grammatik für Datum, Uhrzeit, Timestamp und Datetime-Intervall-literalen Aufrufe von Skalarfunktionen, **wie** Prädikat-Escape-Zeichen, äußere Joins und Prozeduraufrufe. Interoperable Anwendungen ausführen können, sollten diese Sequenzen möglichst verwenden.  
  
 Um festzustellen, ob ein Treiber die Escapesequenzen für Datum, Uhrzeit, Timestamp- oder Datetime-Intervall-Literale unterstützt, eine Anwendung ruft **SQLGetTypeInfo**. Wenn die Datenquelle ein Datum, Uhrzeit, Timestamp- oder Intervall-Datentyp "DateTime" unterstützt, muss es auch die entsprechende Escapesequenz unterstützen. Um zu bestimmen, ob die Escape-Sequenzen unterstützt werden, eine Anwendung ruft **SQLGetInfo**.  
  
 Weitere Informationen finden Sie unter [Escapesequenzen in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)weiter unten in diesem Abschnitt.

