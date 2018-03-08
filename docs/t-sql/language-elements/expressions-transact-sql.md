---
title: "Ausdrücke (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Boolean expressions
- expressions [SQL Server], about expressions
- combining expressions
- Transact-SQL expressions
- expressions [SQL Server], combining
- simple expressions [SQL Server]
- complex expressions [SQL Server]
ms.assetid: ee53c5c8-e36c-40f9-8cd1-d933791b98fa
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 49efa9c940ff4428747942c88259bdd58b96a658
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="expressions-transact-sql"></a>Ausdrücke (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine Kombination aus Symbolen und Operatoren, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] auswertet, um einen einzelnen Datenwert zu erhalten. Einfache Ausdrücke können aus einzelnen Konstanten, Variablen, Spalten oder Skalarfunktionen bestehen. Mithilfe von Operatoren können zwei oder mehrere einfache Ausdrücke zu einem komplexen Ausdruck verknüpft werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
{ constant | scalar_function | [ table_name. ] column | variable   
    | ( expression ) | ( scalar_subquery )   
    | { unary_operator } expression   
    | expression { binary_operator } expression   
    | ranking_windowed_function | aggregate_windowed_function  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Expression in a SELECT statement  
<expression> ::=   
{  
    constant   
    | scalar_function   
    | column  
    | variable  
    | ( expression  )  
    | { unary_operator } expression   
    | expression { binary_operator } expression   
}  
[ COLLATE Windows_collation_name ]  
  
-- Scalar Expression in a DECLARE, SET, IF…ELSE, or WHILE statement  
<scalar_expression> ::=  
{  
    constant   
    | scalar_function   
    | variable  
    | ( expression  )  
    | (scalar_subquery )  
    | { unary_operator } expression   
    | expression { binary_operator } expression   
}  
[ COLLATE { Windows_collation_name ]  
  
```  
  
## <a name="arguments"></a>Argumente  
  
|Begriff|Definition|  
|----------|----------------|  
|*constant*|Ein Symbol, das einen einzelnen bestimmten Datenwert darstellt. Weitere Informationen finden Sie unter [Konstanten &#40; Transact-SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).|  
|*scalar_function*|Ist eine Einheit der [!INCLUDE[tsql](../../includes/tsql-md.md)] Syntax, die einen bestimmten Dienst bereitstellt und einen einzelnen Wert zurückgibt. *Scalar_function* integrierte Skalarfunktion, z. B. der Funktionen SUM, GETDATE oder CAST oder skalare benutzerdefinierte Funktionen werden können.|  
|[ *table_name***.** ]|Der Name oder Alias einer Tabelle.|  
|*column*|Ist der Name einer Spalte. Nur der Name der Spalte ist in einem Ausdruck zulässig.|  
|*variable*|Der Name einer Variablen oder eines Parameters. Weitere Informationen finden Sie unter [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).|  
|**(** *Ausdruck***)** |Ein beliebiger gültiger Ausdruck, wie er in diesem Thema definiert ist. Die Klammern sind gruppierende Operatoren, die sicherstellen, dass alle Operatoren in dem in Klammern stehenden Ausdruck ausgewertet werden, bevor der resultierende Ausdruck mit einem weiteren Ausdruck kombiniert wird.|  
|**(** *scalar_subquery* **)**|Eine Unterabfrage, die einen Wert zurückgibt. Beispiel:<br /><br /> `SELECT MAX(UnitPrice)`<br /><br /> `FROM Products`|  
|{ *unary_operator* }|Unäre Operatoren können nur auf Ausdrücke angewendet werden, die zu einem der Datentypen in der numerischen Datentypkategorie ausgewertet werden. Ein Operator, der nur einen numerischen Operanden besitzt:<br /><br /> + zeigt eine positive Zahl an.<br /><br /> - zeigt eine negative Zahl an.<br /><br /> ~ zeigt den Einserkomplementoperator an.|  
|{ *binary_operator* }|Ein Operator, der die Art und Weise definiert, in der zwei Ausdrücke kombiniert werden, um ein einzelnes Resultat zu liefern. *Binary_operator* kann ein arithmetischer Operator, der Zuweisungsoperator (=), ein bitweiser Operator, ein Vergleichsoperator, ein logischer Operator, der Operator für zeichenfolgenverkettung (+) oder ein unäroperator sein. Weitere Informationen zu Operatoren finden Sie unter [Operatoren &#40; Transact-SQL &#41; ](../../t-sql/language-elements/operators-transact-sql.md).|  
|*ranking_windowed_function*|Eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Rangfolgefunktion. Weitere Informationen finden Sie unter [Rangfolge Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/ranking-functions-transact-sql.md).|  
|*aggregate_windowed_function*|Eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Aggregatfunktion mit der OVER-Klausel. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).|  
  
## <a name="expression-results"></a>Ergebnisse von Ausdrücken  
 Bei einfachen Ausdrücken, die aus einer einzelnen Konstante, Variablen, Skalarfunktion oder einem Spaltennamen bestehen, entsprechen Datentyp, Sortierung, Genauigkeit, Anzahl der Dezimalstellen und Wert des Ausdrucks den jeweiligen Eigenschaften (Datentyp, Sortierung, Genauigkeit usw.) des Elements, auf das verwiesen wird.  
  
 Werden zwei Ausdrücke mithilfe von Vergleichs- oder logischen Operatoren kombiniert, ist das Ergebnis vom booleschen Datentyp. Das Ergebnis nimmt einen der folgenden Werte an: TRUE, FALSE oder UNKNOWN. Weitere Informationen zu booleschen Datentypen finden Sie unter [Vergleichsoperatoren &#40; Transact-SQL &#41; ](../../t-sql/language-elements/comparison-operators-transact-sql.md).  
  
 Werden zwei Ausdrücke mithilfe von arithmetischen Operatoren, bitweisen Operatoren oder Zeichenfolgenoperatoren kombiniert, bestimmt der Operator den resultierenden Datentyp.  
  
 Komplexe Ausdrücke, die aus vielen Symbolen und Operatoren bestehen, werden zu einem Ergebnis mit genau einem Wert ausgewertet. Der Datentyp, die Sortierung, die Genauigkeit und der Wert des resultierenden Ausdrucks werden bestimmt, indem immer jeweils zwei Teilausdrücke kombiniert und ausgewertet werden, bis ein Endergebnis erreicht ist. Die Reihenfolge, in der die Ausdrücke kombiniert werden, ist durch die Rangfolge der Operatoren im Ausdruck definiert.  
  
## <a name="remarks"></a>Hinweise  
 Zwei Ausdrücke können mit einem Operator kombiniert werden, wenn die Datentypen beider Ausdrücke vom Operator unterstützt werden und mindestens eine der folgenden Bedingungen erfüllt ist:  
  
-   Die Ausdrücke besitzen den gleichen Datentyp.  
  
-   Der Datentyp niedrigerer Rangfolge kann implizit in den Datentyp höherer Rangfolge konvertiert werden.  
  
 Falls die Ausdrücke diese Bedingungen nicht erfüllen, kann mit den Funktionen CAST oder CONVERT der Datentyp niedrigerer Rangfolge explizit in den Datentyp höherer Rangfolge konvertiert werden oder in einen dazwischen liegenden Datentyp, der implizit in den Datentyp höherer Rangfolge konvertiert werden kann.  
  
 Falls weder die implizite noch die explizite Konvertierung unterstützt wird, können die beiden Ausdrücke nicht kombiniert werden.  
  
 Die Sortierung eines Ausdrucks, der zu einer Zeichenfolge ausgewertet wird, wird entsprechend den Regeln zur Sortierungsrangfolge festgelegt. Weitere Informationen finden Sie unter [Rangfolge von Sortierungen &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
 In einer Programmiersprache wie C oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], ein Ausdruck immer zu einem einzelnen Ergebnis ausgewertet wird. Für Ausdrücke in einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Auswahlliste gilt eine Abwandlung dieser Regel: Der Ausdruck wird für jede Zeile des Resultsets einzeln ausgewertet. Ein einzelner Ausdruck kann für jede Zeile im Resultset einen anderen Wert annehmen, aber jede Zeile hat nur genau einen Wert für den Ausdruck. In der folgenden `SELECT`-Anweisung sind beispielsweise sowohl der Verweis auf `ProductID` als auch der Term `1+2` in der Auswahlliste Ausdrücke:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, 1+2  
FROM Production.Product;  
GO  
```  
  
 Der Ausdruck `1+2` wird für jede Zeile des Resultsets zu `3` ausgewertet. Obwohl der Ausdruck `ProductID` für jede Zeile des Resultsets einen eindeutigen Wert erzeugt, besitzt jede Zeile nur genau einen Wert für `ProductID`.  
  
## <a name="see-also"></a>Siehe auch  
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Die Rangfolge der Datentypen &#40; Transact-SQL &#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [NULLIF &#40;Transact-SQL&#41;](../../t-sql/language-elements/nullif-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
