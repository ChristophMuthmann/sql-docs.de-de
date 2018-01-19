---
title: EXCEPT und INTERSECT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTERSECT_TSQL
- EXCEPT_TSQL
- INTERSECT
- EXCEPT
dev_langs: TSQL
helpviewer_keywords:
- EXCEPT operator [Transact-SQL]
- queries [SQL Server], comparing
- comparing queries
- INTERSECT operator
ms.assetid: b1019300-171a-4a1a-854f-e1e751de3565
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 706aeaab949399ab6d235a368fa354c32cc54d98
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="set-operators---except-and-intersect-transact-sql"></a>Mengenoperatoren - außer und INTERSECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt durch den Vergleich zweier Abfragen eindeutige Zeilen zurück.  
  
 EXCEPT gibt eindeutige Zeilen aus der linken Eingabeabfrage zurück, die nicht von der rechten Eingabeabfrage ausgegeben werden.  
  
 INTERSECT gibt eindeutige Zeilen, die von der linken und rechten eingabeabfragen-Operator ausgegeben werden.  
  
 Die grundlegenden Regeln für das Kombinieren der Resultsets zweier Abfragen, die EXCEPT oder INTERSECT verwenden, sind die folgenden:  
  
-   Die Anzahl und die Reihenfolge der Spalten müssen für alle Abfragen identisch sein.  
  
-   Die Datentypen müssen kompatibel sein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>Argumente  
 \<*query_specification*> | ( \<*query_expression*> )  
 Eine Abfrageangabe oder ein Abfrageausdruck, die bzw. der Daten zurückgibt, die mit den Daten aus einer anderen Abfrageangabe oder einem anderen Abfrageausdruck zu vergleichen sind. Die Definitionen der Spalten, die Bestandteil eines EXCEPT- oder INTERSECT-Vorgangs sind, müssen nicht identisch, jedoch mithilfe impliziter Konvertierung vergleichbar sein. Wenn sich die Datentypen unterscheiden, der Typ, der verwendet wird, um den Vergleich und Zurückgeben von Ergebnissen gemäß den Regeln für [Rangfolge der Datentypen](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
 Wenn die Typen identisch sind, diese sich aber in der Genauigkeit, Dezimalstellenanzahl oder Länge unterscheiden, wird das Ergebnis basierend auf denselben Regeln wie für das Kombinieren von Ausdrücken bestimmt. Weitere Informationen finden Sie unter [Genauigkeit, Dezimalstellen und Länge &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 Die Abfrageangabe bzw. der Ausdruck kann nicht zurückgeben **Xml**, **Text**, **Ntext**, **Image**, oder nichtbinäre CLR UDT-Spalten Da diese Datentypen nicht vergleichbar sind.  
  
 EXCEPT  
 Gibt alle unterschiedlichen Werte aus der Abfrage links vom EXCEPT-Operator, die auch nicht aus der rechten Abfrage zurückgegeben werden.  
  
 INTERSECT  
 Gibt alle eindeutigen Werte zurück, die von den Abfragen auf der linken und rechten Seite des INTERSECT-Operators zurückgegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Datentypen der vergleichbaren Spalten, die von den Abfragen, links zurückgegeben werden und rechts von den EXCEPT- oder INTERSECT-Operatoren Zeichendatentypen mit unterschiedlichen Sortierungen sind, erfolgt der erforderliche Vergleich gemäß den Regeln der [ Rangfolge von Sortierungen](../../t-sql/statements/collation-precedence-transact-sql.md). Wenn diese Konvertierung nicht ausgeführt werden kann, gibt [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] einen Fehler zurück.  
  
 Wenn Sie zum Bestimmen EINDEUTIGER Zeilen Spaltenwerte vergleichen, werden zwei NULL-Werte als identisch betrachtet.  
  
 Die Spaltennamen des Resultsets, die von EXCEPT oder INTERSECT zurückgegeben werden, sind mit den Namen identisch, die von der linken Abfrage des Operators zurückgegeben wurden.  
  
 Spaltennamen oder -aliasse in ORDER BY-Klauseln müssen auf Spaltennamen verweisen, die von der linken Abfrage zurückgegeben werden.  
  
 Die NULL-Zulässigkeit aller Spalten des Resultsets, die von EXCEPT oder INTERSECT zurückgegeben wird, entspricht der NULL-Zulässigkeit der entsprechenden Spalte, die von der linken Abfrage des Operators zurückgegeben wird.  
  
 Wenn EXCEPT oder INTERSECT zusammen mit anderen Operatoren in einem Ausdruck verwendet wird, wird dieser in der folgenden Rangfolge ausgewertet:  
  
1.  Ausdrücke in Klammern  
  
2.  Der INTERSECT-Operator  
  
3.  EXCEPT und UNION werden auf der Grundlage ihrer Position im Ausdruck von links nach rechts ausgewertet.  
  
 Wenn EXCEPT oder INTERSECT verwendet wird, um mehr als zwei Sätze von Abfragen zu vergleichen, wird die Datentypkonvertierung bestimmt, indem zwei Abfragen nacheinander verglichen werden. Dies erfolgt gemäß der zuvor erwähnten Regeln der Ausdrucksauswertung.  
  
 EXCEPT und INTERSECT können nicht in verteilten partitionierten Sichtdefinitionen und Abfragebenachrichtigungen verwendet werden.  
  
 EXCEPT und INTERSECT können in verteilten Abfragen verwendet werden. Sie werden jedoch nur auf dem lokalen Server ausgeführt und nicht mithilfe eines Push-Vorgangs an den Verbindungsserver übertragen. Daher kann sich das Verwenden von EXCEPT und INTERSECT in verteilten Abfragen auf die Leistung auswirken.  
  
 Vorwärtscursor und statische Cursor werden im Resultset vollständig unterstützt, wenn Sie mit einem EXCEPT- oder INTERSECT-Vorgang verwendet werden. Wenn ein keysetgesteuerter oder dynamischer Cursor zusammen mit einem EXCEPT- oder INTERSECT-Vorgang verwendet wird, wird der Cursor des Resultsets des Vorgangs in einen statischen Cursor konvertiert.  
  
 Wenn ein EXCEPT-Vorgang angezeigt wird, mithilfe der Grafischen showplanfunktion in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], wird der Vorgang als eine [anti Semi Join Links](../../relational-databases/showplan-logical-and-physical-operators-reference.md), und ein INTERSECT-Vorgang wird als eine [left Semi Join](../../relational-databases/showplan-logical-and-physical-operators-reference.md).  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden die Verwendung der `INTERSECT` und `EXCEPT` Operatoren. Die erste Abfrage gibt alle Werte aus der `Production.Product`-Tabelle zum Vergleich mit den Ergebnissen mit `INTERSECT` und `EXCEPT` zurück.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product ;  
--Result: 504 Rows  
```  
  
 Die folgende Abfrage gibt alle eindeutigen Werte zurück, die von den Abfragen auf der linken und rechten Seite des `INTERSECT`-Operators zurückgegeben werden.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
INTERSECT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 238 Rows (products that have work orders)  
```  
  
 Die folgende Abfrage gibt alle eindeutigen Werte aus der linken Abfrage des `EXCEPT`-Operators zurück, die nicht in der rechten Abfrage gefunden werden.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
EXCEPT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 266 Rows (products without work orders)  
```  
  
 Die folgende Abfrage gibt alle eindeutigen Werte aus der linken Abfrage des `EXCEPT`-Operators zurück, die nicht in der rechten Abfrage gefunden werden. Die Tabellen sind die Umkehrung des vorherigen Beispiels.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.WorkOrder  
EXCEPT  
SELECT ProductID   
FROM Production.Product ;  
--Result: 0 Rows (work orders without products)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 In den folgenden Beispielen wird die Verwendung der Operatoren `INTERSECT` und `EXCEPT` veranschaulicht. Die erste Abfrage gibt alle Werte aus der `FactInternetSales`-Tabelle zum Vergleich mit den Ergebnissen mit `INTERSECT` und `EXCEPT` zurück.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales;  
--Result: 60398 Rows  
```  
  
 Die folgende Abfrage gibt alle eindeutigen Werte zurück, die von den Abfragen auf der linken und rechten Seite des `INTERSECT`-Operators zurückgegeben werden.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
INTERSECT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9133 Rows (Sales to customers that are female.)  
```  
  
 Die folgende Abfrage gibt alle eindeutigen Werte aus der linken Abfrage des `EXCEPT`-Operators zurück, die nicht in der rechten Abfrage gefunden werden.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
EXCEPT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9351 Rows (Sales to customers that are not female.)  
```  
  
  

