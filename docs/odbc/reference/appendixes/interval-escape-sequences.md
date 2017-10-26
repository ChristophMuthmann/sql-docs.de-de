---
title: Intervallescapesequenzen | Microsoft Docs
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
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8088c0cb3f85b375423f636d2def8c08c04bbe28
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="interval-escape-sequences"></a>Intervallescapesequenzen
ODBC verwendet Escapesequenzen für die Intervall-Literale. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
 {*Intervall-Literal*}  
  
 Für die BNF-Syntax der *Intervall-Literal*, finden Sie unter der [Intervall Literal Syntax](../../../odbc/reference/appendixes/interval-literal-syntax.md) Abschnitt weiter unten in diesem Anhang.  
  
 Die Intervall-literal-Escapesequenz wird unterstützt, wenn die Interval-Datentypen von der Datenquelle unterstützt werden. Eine Anwendung sollte Aufrufen **SQLGetTypeInfo** um zu bestimmen, ob dieser Datentypen unterstützt werden.

