---
title: CHECKSUM_AGG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b202009c2920dfbcdd068ec3d7ab95de13caa7b4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Prüfsumme der Werte in einer Gruppe zurück. NULL-Werte werden ignoriert. Kann folgen der [OVER-Klausel](../../t-sql/queries/select-over-clause-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>Argumente  
**ALL**  
Wendet die Aggregatfunktion auf alle Werte an. ALL ist die Standardeinstellung.
  
DISTINCT  
Gibt an, dass CHECKSUM_AGG die Prüfsumme von eindeutigen Werten zurückgeben soll.
  
*expression*  
Eine ganze Zahl [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md). Aggregatfunktionen und Unterabfragen sind nicht zulässig.
  
## <a name="return-types"></a>Rückgabetypen
Gibt die Prüfsumme aller *Ausdruck* -Werte als **Int**.
  
## <a name="remarks"></a>Hinweise  
Mithilfe von CHECKSUM_AGG können Änderungen in einer Tabelle erkannt werden.
  
Die Reihenfolge der Zeilen in einer Tabelle hat keinen Einfluss auf das Ergebnis von CHECKSUM_AGG. CHECKSUM_AGG-Funktionen können auch mit dem DISTINCT-Schlüsselwort und der GROUP BY-Klausel verwendet werden.
  
Wenn sich einer der Werte in der Liste mit Ausdrücken ändert, ändert sich gewöhnlich auch die Prüfsumme der Liste. Es besteht jedoch eine geringe Möglichkeit, dass sich die Prüfsumme nicht ändert.
  
CHECKSUM_AGG hat eine ähnliche Funktionalität mit anderen Aggregatfunktionen. Weitere Informationen finden Sie unter [Aggregatfunktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird `CHECKSUM_AGG` verwendet, um Änderungen in der `Quantity`-Spalte der `ProductInventory`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zu erkennen.
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>Siehe auch
[CHECKSUM &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[Failover-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

