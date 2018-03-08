---
title: Angeben einer Achse in einem Pfadausdrucksschritt | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
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
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44ae49e51ac3fab0ca4b2cd8363601a14a3edf0b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="path-expressions---specifying-axis"></a>Path-Ausdrücken - Achse angeben
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Ein Achsenschritt in einem Pfadausdruck besteht aus den folgenden Komponenten:  
  
-   Einer Achse  
  
-   Ein [Knotentest](../xquery/path-expressions-specifying-node-test.md)  
  
-   [0 (null) oder mehr schrittqualifizierern (optional)](../xquery/path-expressions-specifying-predicates.md)  
  
 Weitere Informationen finden Sie unter [Pfadausdrücke &#40; XQuery &#41; ](../xquery/path-expressions-xquery.md).  
  
 Die XQuery-Implementierung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt folgende Achsenschritte:  
  
|Axis|Description|  
|----------|-----------------|  
|**child**|Gibt die untergeordneten Elemente des Kontextknotens zurück.|  
|**descendant**|Gibt alle nachfolgenden Elemente des Kontextknotens zurück.|  
|**parent**|Gibt das übergeordnete Element des Kontextknotens zurück.|  
|**attribute**|Gibt die Attribute des Kontextknotens zurück.|  
|**self**|Gibt den Kontextknoten selbst zurück.|  
|**descendant-or-self**|Gibt den Kontextknoten und alle nachfolgenden Elemente des Kontextknotens zurück.|  
  
 Alle diese Achsen, mit Ausnahme der **übergeordneten** Achse sind vorwärtsgerichtete Achsen. Die **übergeordneten** Achse ist eine rückwärtsgerichtete Achse, da er rückwärts in der Dokumenthierarchie sucht. Beispiel: Der relative Pfadausdruck `child::ProductDescription/child::Summary` enthält zwei Schritte, von denen jeder eine `child`-Achse angibt. Der erste Schritt Ruft die \<ProductDescription >-Elemente des Kontextknotens. Für jede \<ProductDescription > Elementknoten, der zweite Schritt Ruft die \<Zusammenfassung > untergeordneten Elementknoten.  
  
 Der relative Pfadausdruck `child::root/child::Location/attribute::LocationID` besitzt drei Schritte. Die ersten beiden Schritte geben jeweils eine `child`-Achse und der dritte die `attribute`-Achse an. Beim Ausführen mit den fertigungsanweisungen XML-Dokumenten in der **Production.ProductModel** Tabelle gibt der Ausdruck den `LocationID` Attribut des der \<Speicherort >-Elementknotens des der \<Stamm > Element.  
  
## <a name="examples"></a>Beispiele  
 Die Abfragebeispiele in diesem Thema werden gegen angegeben **Xml** in Spalten vom Typ der **AdventureWorks** Datenbank.  
  
### <a name="a-specifying-a-child-axis"></a>A. Angeben einer child-Achse  
 Für ein bestimmtes Produktmodell die folgende Abfrage ruft die \<Features > untergeordneten Elementknoten des der \<ProductDescription > Elementknoten aus der produktkatalogbeschreibung, die in gespeicherten der `Production.ProductModel` Tabelle.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die `query()` Methode der **Xml** -Datentyp, gibt den Path-Ausdruck.  
  
-   Beide Schritte des Pfadausdrucks geben eine `child`-Achse und die Knotennamen `ProductDescription` und `Features` als Knotentests an. Informationen zu Knotentests finden Sie unter [Knotentest angeben, in einem Pfadausdrucksschritt](../xquery/path-expressions-specifying-node-test.md).  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. Angeben von descendant- und descendant-or-self-Achsen  
 In diesem Beispiel werden descendant- und descendant-or-self-Achsen verwendet. Die Abfrage in diesem Beispiel wird angegeben, für eine **Xml** Typvariablen. Die XML-Instanz wird hier zur Veranschaulichung der Unterschiede in den generierten Ergebnissen vereinfacht dargestellt.  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 Im folgenden Ergebnis gibt der Ausdruck einen untergeordneten Elementknoten `<b>` eines Elementknotens `<a>` zurück.  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 Wenn Sie in diesem Ausdruck eine descendant-Achse für den Pfadausdruck angeben,  
  
 `/child::a/child::b/descendant::*`, rufen Sie damit alle nachfolgenden Elemente des <`b`>-Elementknotens ab.  
  
 Das Sternchen (*) im Knotentest stellt den Knotennamen als Knotentest dar. Folglich bestimmt der Typ des Primärknotens der descendant-Achse (der Elementknoten) den Typ der zurückgegebenen Knoten, d. h. in diesem Fall, dass der Ausdruck alle Elementknoten zurückgibt. Es werden keine Textknoten zurückgegeben. Weitere Informationen zum Typ des primären Knotens und seine Beziehung mit der Knotentest finden Sie unter [angeben von Knoten in einem Pfadausdrucksschritt testen](../xquery/path-expressions-specifying-node-test.md) Thema.  
  
 Wie im folgenden Ergebnis gezeigt, werden die Elementknoten <`c`> und <`d`> zurückgegeben:  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 Wenn Sie eine descendant-or-self-Achse statt einer descendant-Achse angeben, gibt `/child::a/child::b/descendant-or-self::*` den Kontextknoten, das Element <`b`>, und seine Nachfolger zurück:  
  
 Dies ist das Ergebnis:  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 Die folgende Beispielabfrage für die **AdventureWorks** Datenbank Ruft alle nachfolgenden Elementknoten des der <`Features`> untergeordneten Elements von der <`ProductDescription`> Element:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. Angeben einer übergeordneten Achse  
 Die folgende Abfrage gibt das untergeordnete <`Summary`>-Element des <`ProductDescription`>-Elements aus dem Produktkatalog-XML-Dokument zurück, das in der `Production.ProductModel`-Tabelle gespeichert ist:  
  
 In diesem Beispiel wird die parent-Achse verwendet, um zu dem übergeordneten Element von <`Feature`> zurückzukehren und das untergeordnete <`Summary`>-Element des <`ProductDescription`>-Elements abzurufen.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 In dieser Beispielabfrage verwendet der Pfadausdruck die `parent`-Achse. Sie können den Ausdruck auch ohne die parent-Achse schreiben, wie im Folgenden gezeigt:  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 Ein nützlicheres Beispiel für die parent-Achse wird im folgenden Beispiel bereitgestellt.  
  
 Jedes Produktmodell-katalogbeschreibung gespeichert, der **CatalogDescription** Spalte die **ProductModel** Tabelle besitzt eine `<ProductDescription>` Element mit der `ProductModelID` Attribut und `<Features>`untergeordnetes Element, wie im folgenden Fragment gezeigt:  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 Die Abfrage legt in der FLWOR-Anweisung eine Iteratorvariable, `$f`, fest, damit die untergeordneten Elemente des `<Features>`-Element zurückgegeben werden. Weitere Informationen finden Sie unter [FLWOR-Anweisung und Iteration &#40; XQuery &#41; ](../xquery/flwor-statement-and-iteration-xquery.md). Für jedes Funktions-Element konstruiert die `return`-Klausel ein XML-Dokument in der folgenden Form:  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 Um die `ProductModelID` für jedes `<Feature`>-Element hinzuzufügen, wird die `parent`-Achse angegeben:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 Beachten Sie, dass dem Pfadausdruck das Prädikat `[1]` hinzugefügt wird, um sicherzustellen, dass ein Singleton-Wert zurückgegeben wird.  
  
  
