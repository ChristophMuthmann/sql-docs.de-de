---
title: Äußere Joins | Microsoft Docs
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
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a350621a056226653a2f9906dbf3931dfdfccec6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="outer-joins"></a>Äußere Joins
ODBC unterstützt die SQL-92 linke, Rechte und vollständige äußere Join-Syntax. Die Escapesequenz für äußere Joins lautet  
  
 **{ABl.** *outer-Joins ***}**  
  
 wobei *äußerer Join* ist  
  
 *Tabellenverweis* {**Links &#124; rechts &#124; vollständige} ÄUßERER JOIN** {*Tabellenverweis* &#124; *äußerer Join*} **ON**  *-Suchbedingung*  
  
 *Tabellenverweis* gibt einen Tabellennamen und *Suchbedingung* gibt die Join-Bedingung zwischen den *Tabellenverweise*.  
  
 Anforderung für einen äußeren Join muss nach angezeigt werden die **FROM** -Schlüsselwort und vor der **, in denen** -Klausel (falls vorhanden). Die vollständige Syntaxinformationen finden Sie unter [äußeren Join Escape Sequence](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) in Anhang C: SQL-Grammatik.  
  
 Die folgenden SQL-Anweisungen erstellen z. B. das gleiche Resultset, das Listet alle Kunden und zeigt die geöffnete Bestellungen aufweist. Die erste Anweisung verwendet die Syntax der Escapesequenz. Die zweite Anweisung verwendet die systemeigene Syntax für Oracle und ist nicht interoperabel.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Um die Arten von äußeren Verknüpfungen zu bestimmen, die eine Datenquelle und die Treiber zu unterstützen, eine Anwendung ruft **SQLGetInfo** mit der SQL_OJ_CAPABILITIES-flag. Die Arten von äußeren Verknüpfungen, die unterstützt werden möglicherweise Links sind, rechts, vollständige oder geschachtelte äußere Joins; äußere Joins in die Namen der Spalte in der **ON** -Klausel müssen sich nicht auf die gleiche Reihenfolge wie ihre entsprechenden Tabellennamen in der **OUTER JOIN** -Klausel; innere Joins zusammen mit äußeren Joins; und äußeren Joins verwenden Jeder Vergleichsoperator für ODBC. Wenn der Typ der SQL_OJ_CAPABILITIES Informationen "0" zurück, wird keine outer Join-Klausel unterstützt.
