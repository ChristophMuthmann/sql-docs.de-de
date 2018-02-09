---
title: "Quantifizierte Ausdrücke (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0efc9fb3b26dd8ebbd7df02609d0570fa67098a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="quantified-expressions-xquery"></a>Quantifizierte Ausdrücke (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die Semantik für auf zwei Sequenzen angewendete boolesche Operatoren unterscheidet sich bei existenziellen und universellen Quantifizierern, wie in der folgenden Tabelle dargestellt.  
  
 *Existenzielle Quantifizierer*  
 Wenn in zwei Sequenzen ein beliebiges Element der ersten Sequenz infolge des verwendeten Vergleichsoperators mit einem Element in der zweiten Sequenz übereinstimmt, ist der zurückgegebene Wert True.  
  
 *Universelle Quantifizierer*  
 Wenn in zwei Sequenzen jedes Element der ersten Sequenz mit einem Element in der zweiten Sequenz übereinstimmt, ist der zurückgegebene Wert True.  
  
 XQuery unterstützt quantifizierte Ausdrücke in der folgenden Form:  
  
```  
( some | every ) <variable> in <Expression> (,…) satisfies <Expression>  
```  
  
 Sie können diese Ausdrücke in einer Abfrage verwenden, um entweder die existenzielle oder die universelle Quantifizierung über eine oder mehrere Sequenzen auf einen Ausdruck anzuwenden. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] muss der Ausdruck in der `satisfies`-Klausel entweder eine Knotensequenz oder eine leere Sequenz oder einen booleschen Wert ergeben. Der effektive boolesche Wert des Ergebnisses dieses Ausdrucks wird dann in der Quantifizierung verwendet. Existenzielle Quantifizierung **einige** gibt "true" zurück, wenn mindestens eine der durch den Quantifizierer gebundenen Werte True ergibt Ausdrucks ist. Universelle Quantifizierung **jeder** muss "true" für alle durch den Quantifizierer gebundenen Werte aufweisen.  
  
 Die folgende Abfrage beispielsweise überprüft jede \<Speicherort > Element, um festzustellen, ob es ein LocationID-Attribut aufweist.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Da LocationID ein erforderliches Attribut des ist die \<Speicherort >-Element, erhalten Sie das erwartete Ergebnis:  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 Anstatt die [Query()-Methode](../t-sql/xml/query-method-xml-data-type.md), können Sie die [Value()-Methode](../t-sql/xml/value-method-xml-data-type.md) um das Ergebnis an die relationale Umgebung zurückzugeben, wie in der folgenden Abfrage gezeigt. Die Abfrage gibt True zurück, wenn alle Arbeitsplatzstandorte LocationID-Attribute besitzen. Anderenfalls gibt die Abfrage False zurück.  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Die folgende Abfrage überprüft, ob eine der Produktabbildungen im Kleinformat vorhanden ist. In den XML-Produktkatalogdaten sind für jedes Produkt Abbildungen aus verschiedenen Winkeln und in verschiedenen Größen gespeichert. Angenommen, Sie möchten sicherstellen, dass alle XML-Produktkatalogdaten mindestens eine Abbildung im Kleinformat enthalten. Dies erreichen Sie mit der folgenden Abfrage:  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Dies ist ein Teilergebnis:  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die Typassertion wird als Teil der Bindung der Variablen in quantifizierten Ausdrücken nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Expressions (XQuery-Ausdrücke)](../xquery/xquery-expressions.md)  
  
  
