---
title: Vergleichsoperatoren (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 45c0e85b89d542dce815104eb8e831169599227b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="comparison-operators-transact-sql"></a>Vergleichsoperatoren (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vergleichsoperatoren testen, ob zwei Ausdrücke gleichwertig sind. Vergleichsoperatoren können für alle Ausdrücke, mit Ausnahme der Ausdrücke verwendet werden die **Text**, **Ntext**, oder **Image** -Datentypen. In der folgenden Tabelle werden die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Vergleichsoperatoren aufgelistet.  
  
|Operator|Bedeutung|  
|--------------|-------------|  
|[= (Ist gleich)](../../t-sql/language-elements/equals-transact-sql.md)|Gleich|  
|[> (Greater Than) (> (Größer als))](../../t-sql/language-elements/greater-than-transact-sql.md)|Größer als|  
|[< (Less Than) (< (Kleiner als))](../../t-sql/language-elements/less-than-transact-sql.md)|Kleiner als|  
|[>= (Greater Than or Equal To) (>= (Größer als oder gleich)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|Größer als oder gleich|  
|[<= (Less Than or Equal To) (<= (Kleiner als oder gleich))](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|Kleiner als oder gleich|  
|[<> (Not Equal To) (<> (Ungleich))](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|Ungleich|  
|[\!= (Ungleich)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|Nicht gleich (kein ISO-Standard)|  
|[\!< (Nicht kleiner als)](../../t-sql/language-elements/not-less-than-transact-sql.md)|Nicht kleiner als (kein ISO-Standard)|  
|[\!> (Nicht größer als)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|Nicht größer als (kein ISO-Standard)|  
  
## <a name="boolean-data-type"></a>Boolesche Datentypen  
 Das Ergebnis eines Vergleichsoperators hat die **booleschen** -Datentyp. Es kann drei Werte annehmen: TRUE, FALSE und UNKNOWN. Ausdrücke, die Zurückgeben einer **booleschen** -Datentyp werden als boolesche Ausdrücke bezeichnet.  
  
 Im Gegensatz zu anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentypen, eine **booleschen** -Datentyp kann nicht mit dem Datentyp einer Spalte oder Variable angegeben werden, und kann nicht in einem Resultset zurückgegeben werden.  
  
 Wenn SET ANSI_NULLS auf ON festgelegt ist, gibt ein Operator mit einem oder zwei NULL-Ausdrücken UNKNOWN zurück. Wenn SET ANSI_NULLS auf OFF festgelegt ist, gelten die gleichen Regeln; allerdings gibt der Gleichheitsoperator (=) TRUE zurück, wenn beide Ausdrücke NULL sind. So gibt beispielsweise NULL = NULL den Wert TRUE zurück, wenn SET ANSI_NULLS auf OFF festgelegt ist.  
  
 Ausdrücke mit **booleschen** -Datentypen werden in der WHERE-Klausel zum Filtern der Zeilen, die für die suchbedingungen und sprachanweisungen Kontrollfluss z. B. IF und WHILE, z. B. infrage kommen verwendet:  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
