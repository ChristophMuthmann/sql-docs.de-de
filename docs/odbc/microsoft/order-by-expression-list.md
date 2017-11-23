---
title: ORDER BY-Ausdruck-Liste | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1650a62190332f6b534b895d1d584bf70347140e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="order-by-expression-list"></a>ORDER BY-Ausdruck-Liste
Ausdrücke können in der ORDER BY-Klausel verwendet werden. Beispielsweise in den folgenden Klauseln in der Tabelle sortiert wird, ist durch drei wichtigsten Ausdrücke: a + b, C + d und e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Keine Reihenfolge ist zulässig, auf die Set-Funktionen oder ein Ausdruck, der eine Set-Funktion enthält.
