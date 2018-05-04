---
title: Parametermarkierungen | Microsoft Docs
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df895c9e9956c1fde178824d1e14030246710946
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers"></a>Parametermarkierungen
In Übereinstimmung mit der SQL-92-Spezifikation platziert keine Anwendung parametermarkierungen in den folgenden Speicherorten. Eine umfangreichere Liste finden Sie in der SQL-92-Spezifikation.  
  
-   In einem **wählen** Liste  
  
-   Beide *Ausdrücke* in einem *Vergleichsprädikat*  
  
-   Als beide Operanden des binären Operators  
  
-   Als ersten und zweiten Operanden von einem **BETWEEN** Vorgang  
  
-   Als das erste und die dritte Operanden ein **BETWEEN** Vorgang  
  
-   Der Ausdruck und den ersten Wert des einem **IN** Vorgang  
  
-   Als Operand ein unäres + "oder" – Vorgang  
  
-   Als Argument einer *Set-Funktionsreferenz*  
  
 Weitere Informationen zu den parametermarkierungen finden Sie unter der SQL-92-Spezifikation. Weitere Informationen zu Parametern finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md).
