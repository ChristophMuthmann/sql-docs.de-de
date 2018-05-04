---
title: ORDER BY-Ausdruck-Liste | Microsoft Docs
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
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e531a26f0436c598fa04acc11e9735bb80faed44
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="order-by-expression-list"></a>ORDER BY-Ausdruck-Liste
Ausdrücke können in der ORDER BY-Klausel verwendet werden. Beispielsweise in den folgenden Klauseln in der Tabelle sortiert wird, ist durch drei wichtigsten Ausdrücke: a + b, C + d und e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Keine Reihenfolge ist zulässig, auf die Set-Funktionen oder ein Ausdruck, der eine Set-Funktion enthält.
