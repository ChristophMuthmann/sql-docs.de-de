---
title: "Genauigkeit, Dezimalstellen und Länge (Transact-SQL) | Microsoft-Dokumentation"
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
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist die maximale Standardgenauigkeit der Datentypen **numeric** und **decimal** 38. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist das Standardmaximum 28.
  
Die Länge für einen numerischen Datentyp ist die Anzahl der Bytes, die zum Speichern der Zahl verwendet werden. Die Länge für einen Zeichenfolgen- oder einen Unicode-Datentyp ist die Anzahl der Zeichen. Die Länge der Datentypen **binary**, **varbinary** und **image** entspricht der Anzahl von Bytes. Ein **int**-Datentyp kann z.B. 10 Stellen enthalten, wird in 4 Bytes gespeichert und nimmt kein Dezimaltrennzeichen an. Der **int**-Datentyp hat eine Genauigkeit von 10 und eine Länge von 4. Er weist 0 Dezimalstellen auf.
  
Wenn zwei Ausdrücke vom Datentyp **char**, **varchar**, **binary** oder **varbinary** verkettet werden, ist die Länge des sich ergebenden Ausdrucks die Summe der Längen der beiden Ausgangsausdrücke, jedoch begrenzt auf 8.000 Zeichen.
  
Wenn zwei Ausdrücke vom Datentyp **nchar** oder **nvarchar** verkettet werden, ist die Länge des sich ergebenden Ausdrucks die Summe der Längen der beiden Ausgangsausdrücke, jedoch begrenzt auf 4.000 Zeichen.
  
Wenn zwei Ausdrücke vom selben Datentyp, aber mit verschiedenen Längen mit UNION, EXCEPT oder INTERSECT verglichen werden, ist die sich ergebende Länge die maximale Länge der beiden Ausdrücke.
  
Genauigkeit und Dezimalstellenanzahl der numerischen Datentypen außer **decimal** sind nicht veränderbar. Wenn ein arithmetischer Operator zwei Ausdrücke vom gleichen Typ verwendet, so ist das Ergebnis vom selben Datentyp; er hat die Genauigkeit und die Dezimalstellenanzahl, die für diesen Datentyp definiert sind. Wenn ein Operator zwei Ausdrücke mit verschiedenen numerischen Datentypen verwendet, bestimmen die Rangfolgeregeln für Datentypen den Datentyp des Ergebnisses. Das Ergebnis hat die für seinen Datentyp definierte Genauigkeit und Dezimalstellenanzahl.
  
Die folgende Tabelle definiert, wie Genauigkeit und Dezimalstellen des Ergebnisses berechnet werden, wenn das Ergebnis einer Operation vom Datentyp **decimal** ist. Das Ergebnis ist vom Datentyp **decimal**, wenn eine der folgenden Bedingungen zutrifft:
-   Beide Ausdrücke sind vom Datentyp **decimal**.  
-   Ein Ausdruck ist vom Datentyp **decimal**, und der andere Ausdruck ist von einem Datentyp mit einer niedrigeren Rangfolge als **decimal**.  
  
Die Operandenausdrücke werden als Ausdruck e1 mit der Genauigkeit p1 und der Dezimalstellenanzahl s1 und Ausdruck e2 mit der Genauigkeit p2 und der Dezimalstellenanzahl s2 bezeichnet. Die Genauigkeit und Dezimalstellenanzahl für einen Ausdruck, der nicht vom Datentyp **decimal** ist, entspricht der für den Datentyp des Ausdrucks definierten Genauigkeit und Dezimalstellenanzahl.
  
|Vorgang|Genauigkeit des Ergebnisses|Dezimalstellen des Ergebnisses *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 { UNION &#124; EXCEPT &#124; INTERSECT } e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\* Die Genauigkeit und Dezimalstellen des Ergebnisses haben ein absolutes Maximum von 38. Wenn die Genauigkeit des Ergebnisses 38 überschreitet, wird es auf 38 reduziert. Ebenfalls wird die zugehörige Dezimalstellenanzahl reduziert, um zu verhindern, dass der ganzzahlige Teil eines Ergebnisses abgeschnitten wird. In solchen Fällen (z.B. bei der Multiplikation oder Division) wird der Skalierungsfaktor nicht reduziert, um die Dezimalgenauigkeit beizubehalten. Dadurch kann jedoch ein Überlauffehler ausgelöst werden.

Bei Additions- und Subtraktionsvorgängen werden `max(p1 – s1, p2 – s2)`-Platzhalter benötigt, um den integralen Bestandteil der Dezimalzahl zu speichern. Wenn nicht genügend Speicherplatz vorhanden ist (d.h. `max(p1 – s1, p2 – s2) < min(38, precision) – scale`), werden die Dezimalstellen reduziert, um genügend Speicherplatz für den integralen Bestandteil bereitzustellen. Die resultierenden Dezimalstellen sind `MIN(precision, 38) - max(p1 – s1, p2 – s2)`. Die Stellen hinter dem Dezimaltrennzeichen werden also möglicherweise gerundet, um in diese zu passen.

Bei Multiplikations- und Divisionsvorgängen werden `precision - scale`-Platzhalter benötigt, um den integralen Bestandteil des Ergebnisses zu speichern. Die Dezimalstellen können mithilfe von folgenden Regeln reduziert werden:
1.  Die resultierenden Dezimalstellen wird auf `min(scale, 38 – (precision-scale))` reduziert, wenn der integrale Bestandteil kleiner als 32 ist, da diese nicht größer als `38 – (precision-scale)` sein darf. Das Ergebnis kann in diesem Fall gerundet werden.
1. Die Dezimalstellen werden nicht geändert, wenn dieses kleiner als 6 und der integrale Bestandteil größer als 32 ist. In diesem Fall wird möglicherweise ein Überlauffehler ausgelöst, wenn das Ergebnis nicht in decimal(38, scale) passt. 
1. Die Dezimalstellen werden auf 6 festgelegt, wenn dieses weniger als 6 beträgt und der integrale Bestandteil größer als 32 ist. In diesem Fall werden der integrale Bestandteil und die Dezimalstellen reduziert, und der sich ergebende Typ lautet decimal(38,6). Das Ergebnis wird auf 6 Dezimalstellen gerundet. Andernfalls wird ein Überlauffehler ausgelöst, wenn der integrale Bestandteil nicht in 32 Ziffern passt.

## <a name="examples"></a>Beispiele
Der folgende Ausdruck gibt das Ergebnis `0.00000090000000000` ohne Rundung zurück, da das Ergebnis in `decimal(38,17)` passt:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
In diesem Fall beträgt die Genauigkeit 61 und die Dezimalstellen betragen 40.
Der integrale Bestandteil (precision-scale = 21) ist kleiner als 32. Dies entspricht also Fall (1) in den Multiplikationsregeln, und die Dezimalstellen werden als `min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17` berechnet. Der Ergebnistyp ist `decimal(38,17)`.

Der folgende Ausdruck gibt das Ergebnis `0.000001` zurück, das in `decimal(38,6)` passen soll:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
In diesem Fall beträgt die Genauigkeit 61 und die Dezimalstellen betragen 20.
Die Dezimalstellen sind größer als 6 und der integrale Bestandteil (`precision-scale = 41`) größer als 32. Dies entspricht also Fall (3) in den Multiplikationsregeln, und der Ergebnistyp ist `decimal(38,6)`.

## <a name="see-also"></a>Siehe auch
[Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
