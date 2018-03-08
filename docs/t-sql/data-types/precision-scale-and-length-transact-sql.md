---
title: "Genauigkeit, Dezimalstellen und Länge (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6f35d99b2bc195aa311e30310787023dfafd4855
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="precision-scale-and-length-transact-sql"></a>Genauigkeit, Dezimalstellen und Länge (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Genauigkeit gibt die Anzahl der Ziffern einer Zahl an. Dezimalstellen gibt die Anzahl der Nachkommastellen an. Die Zahl 123,45 hat z. B. eine Genauigkeit von 5 und 2 Dezimalstellen.
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die maximale standardgenauigkeit der **numerischen** und **decimal** Datentypen ist 38. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist das Standardmaximum 28.
  
Die Länge für einen numerischen Datentyp ist die Anzahl der Bytes, die zum Speichern der Zahl verwendet werden. Die Länge für einen Zeichenfolgen- oder einen Unicode-Datentyp ist die Anzahl der Zeichen. Die Länge für **binäre**, **Varbinary**, und **Image** Datentypen wird die Anzahl der Bytes. Angenommen, ein **Int** Datentyp können 10 Stellen enthalten, wird in 4 Bytes gespeichert und akzeptiert keine Dezimaltrennzeichen an. Die **Int** Datentyp hat eine Genauigkeit von 10, eine Länge von 4 und einer Skala von 0.
  
Wenn zwei **Char**, **Varchar**, **binäre**, oder **Varbinary** verkettet werden, ist die Länge des sich ergebenden Ausdrucks die Summe der Längen der beiden 8.000 Zeichen, welcher Wert kleiner ist.
  
Wenn zwei **Nchar** oder **Nvarchar** verkettet werden, die Länge des sich ergebenden Ausdrucks ist die Summe der Längen der beiden 4.000 Zeichen, welcher Wert kleiner ist.
  
Wenn zwei Ausdrücke vom selben Datentyp, aber mit verschiedenen Längen mit UNION, EXCEPT oder INTERSECT verglichen werden, ist die sich ergebende Länge die maximale Länge der beiden Ausdrücke.
  
Die Genauigkeit und Dezimalstellenanzahl der numerischen Datentypen außer **decimal** behoben werden. Wenn ein arithmetischer Operator zwei Ausdrücke vom gleichen Typ verwendet, so ist das Ergebnis vom selben Datentyp; er hat die Genauigkeit und die Dezimalstellenanzahl, die für diesen Datentyp definiert sind. Wenn ein Operator zwei Ausdrücke mit verschiedenen numerischen Datentypen verwendet, bestimmen die Rangfolgeregeln für Datentypen den Datentyp des Ergebnisses. Das Ergebnis hat die für seinen Datentyp definierte Genauigkeit und Dezimalstellenanzahl.
  
In der folgenden Tabelle definiert, wie die Genauigkeit und Dezimalstellen des Ergebnisses berechnet werden, wenn das Ergebnis eines Vorgangs des Typs ist **decimal**. Das Ergebnis ist **decimal** Wenn eine der folgenden Aussagen zutrifft:
-   Beide Ausdrücke **decimal**.  
-   Ein Ausdruck ist **decimal** und der andere einen Datentyp mit einer geringeren Priorität als **decimal**.  
  
Die Operandenausdrücke werden als Ausdruck e1 mit der Genauigkeit p1 und der Dezimalstellenanzahl s1 und Ausdruck e2 mit der Genauigkeit p2 und der Dezimalstellenanzahl s2 bezeichnet. Die Genauigkeit und Dezimalstellenanzahl für einen Ausdruck, der nicht **decimal** ist die Genauigkeit und Dezimalstellenanzahl, die für den Datentyp des Ausdrucks definiert.
  
|Vorgang|Genauigkeit des Ergebnisses|Dezimalstellen des Ergebnisses *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|E1 {UNION &#124; AUßER &#124; INTERSECT} e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\*Die Genauigkeit und Dezimalstellenanzahl haben ein absolutes Maximum von 38. Wenn die Genauigkeit des Ergebnisses 38 überschreitet, wird reduziert, bis 38, und die zugehörige Dezimalstellenanzahl reduziert, um zu versuchen, die verhindern, dass des ganzzahligen Teils eines Ergebnisses abgeschnitten wird. In einigen Fällen wie Multiplikation oder Division wird Skalierungsfaktor nicht verringert werden um bleiben Dezimalstellen, obwohl Ganzzahlüberlauf-Fehler ausgelöst werden kann.

In Addition und Subtraktion Vorgänge müssen wir `max(p1 – s1, p2 – s2)` stellen integralen Bestandteil der Dezimalzahl zu speichern. Wenn es nicht genügend Speicherplatz zum Speichern von ihnen also ist `max(p1 – s1, p2 – s2) < min(38, precision) – scale`, die Dezimalstellenanzahl reduziert, um ausreichend Speicherplatz für integraler Bestandteil bereitzustellen. Ist der resultierende Skalierung `MIN(precision, 38) - max(p1 – s1, p2 – s2)`, also der Teil mit Bruchzahlen enthält entsprechend in die resultierende Dezimalstellen gerundet werden kann.

In Multiplikationen und Divisionen müssen wir `precision - scale` Stellen zum Speichern des ganzzahligen Teils des Ergebnisses. Die Skalierung möglicherweise reduziert werden, mithilfe der folgenden Regeln:
1.  Die resultierende Dezimalstellenanzahl reduziert, um `min(scale, 38 – (precision-scale))` das ganzzahlige Teil kleiner als 32, ist, da er ist größer als `38 – (precision-scale)`. In diesem Fall möglicherweise Ergebnis gerundet.
1. Die Skalierung wird nicht geändert werden, wenn er kleiner als 6 ist und das ganzzahlige Teil größer als 32 ist. In diesem Fall möglicherweise Ganzzahlüberlauf-Fehler ausgelöst, wenn er nicht in Decimal (38, Skala) passen 
1. Die Skalierung wird auf 6 festgelegt werden, wenn sie größer als 6 ist und das ganzzahlige Teil größer als 32 ist. In diesem Fall integraler Bestandteil und Skalierung zu reduzieren und sich ergebenden Typ decimal(38,6). Ergebnis mit 6 Dezimalstellen gerundet werden kann, oder Ganzzahlüberlauf-Fehler wird ausgelöst, wenn integraler Bestandteil nicht in 32 Ziffern passen.

## <a name="examples"></a>Beispiele
Der folgende Ausdruck gibt Ergebnis `0.00000090000000000` ohne runden, da das Ergebnis in einem Platz finden `decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
In diesem Fall ist mit einfacher Genauigkeit 61 und Skalierung ist 40.
Integraler Bestandteil (Genauigkeit skalierter = 21) ist kleiner als 32, sodass dies Schreibweise (1) im Multiplikation Regeln ist und Skalierung als berechnet wird `min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`. Ist der Ergebnistyp `decimal(38,17)`.

Der folgende Ausdruck gibt Ergebnis `0.000001` übersteigt `decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
In diesem Fall ist mit einfacher Genauigkeit 61 und Dezimalstellen ist 20.
Skalierung ist größer als 6 und ganzzahligen Teil (`precision-scale = 41`) ist größer als 32. Dies ist der Fall (3) in den Regeln für Multiplikation und Ergebnistyp ist `decimal(38,6)`.

## <a name="see-also"></a>Siehe auch
[Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
