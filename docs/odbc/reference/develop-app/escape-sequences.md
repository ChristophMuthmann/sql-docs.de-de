---
title: Escape-Zeichensequenzen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 716c304225e71455a6c492e9824712806f83e3a8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="escape-sequences"></a>Escapesequenzen
ODBC definiert Escapesequenzen, die mit standard-Grammatik für Datum, Uhrzeit, Timestamp und Datetime-Intervall-literalen Aufrufe von Skalarfunktionen, **wie** Prädikat-Escape-Zeichen, äußere Joins und Prozeduraufrufe. Interoperable Anwendungen ausführen können, sollten diese Sequenzen möglichst verwenden.  
  
 Um festzustellen, ob ein Treiber die Escapesequenzen für Datum, Uhrzeit, Timestamp- oder Datetime-Intervall-Literale unterstützt, eine Anwendung ruft **SQLGetTypeInfo**. Wenn die Datenquelle ein Datum, Uhrzeit, Timestamp- oder Intervall-Datentyp "DateTime" unterstützt, muss es auch die entsprechende Escapesequenz unterstützen. Um zu bestimmen, ob die Escape-Sequenzen unterstützt werden, eine Anwendung ruft **SQLGetInfo**.  
  
 Weitere Informationen finden Sie unter [Escapesequenzen in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)weiter unten in diesem Abschnitt.
