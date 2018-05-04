---
title: Intervallescapesequenzen | Microsoft Docs
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
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3973a5149aa5861b2d194cd4487a15b0f97e7f94
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="interval-escape-sequences"></a>Intervallescapesequenzen
ODBC verwendet Escapesequenzen für die Intervall-Literale. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
 {*Intervall-Literal*}  
  
 Für die BNF-Syntax der *Intervall-Literal*, finden Sie unter der [Intervall Literal Syntax](../../../odbc/reference/appendixes/interval-literal-syntax.md) Abschnitt weiter unten in diesem Anhang.  
  
 Die Intervall-literal-Escapesequenz wird unterstützt, wenn die Interval-Datentypen von der Datenquelle unterstützt werden. Eine Anwendung sollte Aufrufen **SQLGetTypeInfo** um zu bestimmen, ob dieser Datentypen unterstützt werden.
