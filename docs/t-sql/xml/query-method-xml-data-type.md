---
title: Query()-Methode (Xml-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4ec43116cf548df0a6f3541ab882635331f1b395
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="query-method-xml-data-type"></a>query()-Methode (xml-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine XQuery-Abfrage für eine Instanz von der **Xml** -Datentyp. Das Ergebnis ist vom **Xml** Typ. Die Methode gibt eine Instanz nicht typisierten XMLs zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>Argumente  
 XQuery  
 Ist eine Zeichenfolge (ein XQuery-Ausdruck), die XML-Knoten wie z. B. element- und attribute-Knoten in einer XML-Instanz abfragt.  
  
## <a name="examples"></a>Beispiele  
 Dieser Abschnitt enthält Beispiele zum Verwenden der Query()-Methode des der **Xml** -Datentyp.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>A. Verwenden der query()-Methode mit einer Variablen vom Typ XML  
 Das folgende Beispiel deklariert eine Variable  **@myDoc**  von **Xml** geben und eine XML-Instanz zugewiesen. Die **query()** Methode wird dann zum Angeben einer XQuery für das Dokument.  
  
 Die Abfrage ruft das untergeordnete <`Features`>-Element des <`ProductDescription`>-Elements ab:  
  
```  
declare @myDoc xml  
set @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. Verwenden der query()-Methode für eine Spalte vom Typ XML  
 Im folgenden Beispiel die **query()** Methode dient zum Angeben einer XQuery für die **CatalogDescription** Spalte **Xml** Geben Sie in der  **AdventureWorks** Datenbank:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die CatalogDescription-Spalte ist eine typisierte **Xml** Spalte. Dies bedeutet, dass ihr eine Schemaauflistung zugeordnet wurde. In der [XQuery-Prolog](../../xquery/modules-and-prologs-xquery-prolog.md), **Namespace** -Schlüsselwort wird verwendet, um das Präfix, das später verwendet wird, im Hauptteil Abfrage zu definieren.  
  
-   Die **query()** -Methode erstellt XML, ein <`Product`> Element mit einer **ProductModelID** -Attribut, in dem die **ProductModelID** Attributwert ist aus der Datenbank abgerufen. Weitere Informationen zu XML-Konstruktion, finden Sie unter [XML-Konstruktion &#40; XQuery &#41; ](../../xquery/xml-construction-xquery.md).  
  
-   Die [EXIST()-Methode (XML-Datentyp)](../../t-sql/xml/exist-method-xml-data-type.md) in die WHERE-Klausel verwendet wird, um nur die Zeilen, die enthält die <`Warranty`>-Element in der XML-Code. In diesem Fall die **Namespace** -Schlüsselwort zum Definieren von zwei Namespacepräfixen verwendet wird.  
  
 Dies ist das Teilergebnis:  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 Beachten Sie, dass die query()- und exist()-Methoden beide das PD-Präfix deklarieren. In diesen Fällen können Sie WITH XMLNAMESPACES verwenden, um zuerst die Präfixe zu definieren und dann in der Abfrage zu verwenden.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
