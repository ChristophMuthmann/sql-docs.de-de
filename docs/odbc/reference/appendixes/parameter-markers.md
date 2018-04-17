---
title: Parametermarkierungen | Microsoft Docs
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c307c188deb2b268174130274f665a168aff2a88
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
