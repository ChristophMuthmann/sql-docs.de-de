---
title: SQL:Variable()-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 77a8f9c8857c0a054922d0ad2bdb4b12ceab815e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery Extension Functions - sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Macht eine Variable verfügbar, die einen relationalen SQL-Wert in einem XQuery-Ausdruck enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>Hinweise  
 In diesem Thema beschriebenen [einbinden relationaler Daten in XML-Daten](../t-sql/xml/binding-relational-data-inside-xml-data.md), Sie können diese Funktion verwenden, bei der Verwendung [XML-Datentypmethoden](../t-sql/xml/xml-data-type-methods.md) zum Verfügbarmachen eines relationalen Werts in XQuery.  
  
 Z. B. die [Query()-Methode](../t-sql/xml/query-method-xml-data-type.md) wird verwendet, um eine Abfrage für eine XML-Instanz angeben, die in gespeichert ist ein **Xml** -Datentyp, Variable oder Spalte. Manchmal sollen in einer Abfrage auch Werte aus einer [!INCLUDE[tsql](../includes/tsql-md.md)]-Variablen oder einem -Parameter verwendet werden, um relationale und XML-Daten zu verbinden. Zu diesem Zweck verwenden Sie die **SQL: Variable** Funktion.  
  
 Der SQL-Wert wird in einen entsprechenden XQuery-Wert zugeordnet werden, und dessen Typ werden ein XQuery-Basistyp, der mit dem entsprechenden SQL-Datentyp entspricht.  
  
 Sie können nur auf verweisen eine **Xml** Instanz im Zusammenhang mit dem quellenausdruck einer XML-DML-insert-Anweisung; andernfalls Sie nicht auf Werte vom Typ verweisen **Xml** oder eine common Language Runtime (CLR) einen benutzerdefinierten Typ.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. Einfügen einer Transact-SQL-Variablen in XML mit der sql:variable()-Funktion  
 Im folgenden Beispiel wird eine XML-Instanz erstellt, die aus Folgendem besteht:  
  
-   Einem Wert (`ProductID`) aus einer Nicht-XML-Spalte. Die [SQL:Column()-Funktion](../xquery/xquery-extension-functions-sql-column.md) zum Binden dieses Werts in der XML-Code verwendet wird.  
  
-   Einem Wert (`ListPrice`) aus einer Nicht-XML-Spalte aus einer anderen Tabelle. Die `sql:column()`-Funktion wird auch hier zum Binden dieses Werts im XML-Code verwendet.  
  
-   Einem Wert (`DiscountPrice`) aus einer [!INCLUDE[tsql](../includes/tsql-md.md)]-Variablen. Zum Binden dieses Werts im XML-Code wird die `sql:variable()`-Methode verwendet.  
  
-   Ein Wert (`ProductModelName`) aus einer **Xml** Typspalte, um die Abfrage interessanter zu gestalten.  
  
 Im Folgenden wird die Abfrage aufgeführt:  
  
```  
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Der XML-Code wird durch die XQuery-Abfrage in der `query()`-Methode erstellt.  
  
-   Die `namespace` Schlüsselwort wird verwendet, um ein Namespacepräfix im Definieren der [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md). Dies geschieht, weil der `ProductModelName`-Attributwert aus der Spalte des `CatalogDescription xml`-Typs abgerufen wird, der ein Schema zugeordnet ist.  
  
 Dies ist das Ergebnis:  
  
```  
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server XQuery-Erweiterungsfunktionen](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Erstellen von Instanzen der XML-Daten](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml-Datentypmethoden](../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
