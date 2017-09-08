---
title: "Allgemeine XQuery Anwendungsfälle | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3a6f20206d0679adeffdc2b504ccef1d010c957b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="general-xquery-use-cases"></a>Allgemeine Einsatzgebiete für XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dieses Thema stellt allgemeine Beispiele für die Verwendung von XQuery zur Verfügung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. Abfragen von Produkten und Gewichten in Katalogbeschreibungen  
 Die folgende Abfrage gibt die Produktmodell-IDs und (sofern vorhanden) die Gewichtungen aus der Produktkatalogbeschreibung zurück. Die Abfrage erstellt XML in der folgenden Form:  
  
```  
<Product ProductModelID="…">  
  <Weight>…</Weight>  
</Product>  
```  
  
 Im Folgenden wird die Abfrage aufgeführt:  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **Namespace** -Schlüsselwort im XQuery-Prolog definiert ein Namespacepräfix, das verwendet wird, im Hauptteil Abfrage.  
  
-   Der Body-Teil der Abfrage bewirkt die Konstruktion des erforderlichen XML-Codes.  
  
-   In der WHERE-Klausel der **exist()** Methode wird verwendet, um nur Zeilen zu suchen, die produktkatalogbeschreibungen enthalten. Dies bedeutet, dass das <`ProductDescription`>-Element im XML enthalten ist.  
  
 Dies ist das Ergebnis:  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 Mit der folgenden Abfrage werden die gleichen Informationen abgerufen, jedoch nur für die Produktmodelle, deren Katalogbeschreibung das Gewicht, das <`Weight`>-Element, in den Spezifikationen, im <`Specifications`>-Element, enthält. In diesem Beispiel wird WITH XLMNAMESPACES zum Deklarieren des pd-Präfixes und seiner Namespacebindung verwendet. Auf diese Weise wird die Bindung nicht in beiden beschrieben die **query()** Methode und in der **exist()** Methode.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 In der vorherigen Abfrage die **exist()** Methode der **Xml** -Datentyp in die WHERE-Klausel überprüft, um festzustellen, ob ein <`Weight`> Element in der <`Specifications`> Element.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. Suchen von Produktmodell-IDs für Produktmodelle, deren Katalogbeschreibungen Bilder mit frontalem Blickwinkel und geringer Größe enthalten  
 Die Produktbilder sind im XML der Produktkatalogbeschreibung im <`Picture`>-Element enthalten. Jedes Bild besitzt mehrere Eigenschaften. Dazu gehören der Bildwinkel, das <`Angle`>-Element, und die Größe, das <`Size`>-Element.  
  
 Für Produktmodelle, deren Katalogbeschreibungen Bilder mit frontalem Blickwinkel und geringer Größe enthalten, konstruiert die Abfrage XML-Code, der die folgende Form aufweist:  
  
```  
< Product ProductModelID="…">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   In der WHERE-Klausel der **exist()** Methode wird verwendet, um nur Zeilen abzurufen, die produktkatalogbeschreibungen mit der <`Picture`> Element.  
  
-   Die WHERE-Klausel verwendet die **value()** Methode zwei Male auf, um die Werte von Vergleichen die <`Size`> und <`Angle`> Elemente.  
  
 Dies ist ein Teilergebnis:  
  
```  
<p1:Product   
  xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. Erstellen Sie eine flache Liste des Produkts Model Name-Funktion-Paare, für jedes Paar eingeschlossen der \<Features >-Element  
 In der Katalogbeschreibung des Produktmodells enthält der XML-Code mehrere Produktfunktionen. All diese Funktionen werden in das <`Features`>-Element eingeschlossen. Die Abfrage verwendet [XML-Konstruktion (XQuery)](../xquery/xml-construction-xquery.md) der erforderlichen XML-Code erstellen. Der Ausdruck in den geschweiften Klammern wird durch das Ergebnis ersetzt.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   $pd/p1:Features/* gibt nur die untergeordneten Elemente des <`Features`>-Knotens zurück; $pd/p1:Features/node() gibt alle Knoten zurück. Das schließt Elementknoten, Textknoten, Verarbeitungsanweisungen und Kommentare ein.  
  
-   Die beiden FOR-Schleifen generieren ein kartesisches Produkt, aus dem der Produktname und die individuelle Funktion zurückgegeben werden.  
  
-   Die **ProductName** ist ein Attribut. Die XML-Konstruktion in dieser Abfrage gibt dieses als ein Element zurück.  
  
 Dies ist ein Teilergebnis:  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. Anhand der katalogbeschreibung eines Produktmodells, Modell-Liste des Produkts Name, Modell-ID und gruppiert Sie Funktionen innerhalb einer \<Product >-Element  
 Mithilfe der Informationen in der katalogbeschreibung des Produktmodells gespeichert, die folgende Abfrage listet produktmodellname, Modell-ID und Funktionen gruppiert innerhalb einer \<Product >-Element.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Dies ist ein Teilergebnis:  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="http://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="http://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. Abrufen von Produktmodell-Funktionsbeschreibungen  
 Die folgende Abfrage erstellt XML mit einem <`Product`>-Element mit **ProducModelID**, **ProductModelName** Attribute und die ersten beiden Produktfunktionen enthält. Genau genommen sind die ersten beiden Produktfunktionen die beiden ersten untergeordneten Elemente des <`Features`>-Elements. Wenn es darüber hinaus weitere Funktionen gibt, gibt die Abfrage ein leeres <`There-is-more/`>-Element zurück.  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die FOR ... RETURN-Schleifenstruktur ruft die ersten beiden Produktfunktionen ab. Die **position()** Funktion wird verwendet, um die Position der Elemente in der Sequenz zu finden.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. Suchen von Elementnamen in der Produktkatalogbeschreibung, die mit "ons" enden  
 Die folgende Abfrage durchsucht die Katalogbeschreibungen und gibt alle Elemente im <`ProductDescription`>-Element zurück, deren Name mit "ons" endet.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Dies ist ein Teilergebnis:  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. Suchen von Zusammenfassungsbeschreibungen mit dem Wort "Aerodynamic"  
 Die folgende Abfrage ruft die Produktmodelle ab, deren Produktbeschreibung das Wort "Aerodynamic" in der zusammenfassenden Beschreibung enthält:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 Beachten Sie, die die SELECT-Abfrage gibt **query()** und **value()** Methoden die **Xml** -Datentyp. Deshalb muss die Namespacedeklaration nicht zweimal in zwei verschiedenen Abfrageprologen wiederholt werden, sondern das Präfix pd wird in der Abfrage verwendet und nur einmal mit WITH XMLNAMESPACES definiert.  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Mit der WHERE-Klausel werden nur die Zeilen abgerufen, für die die Katalogbeschreibung das Wort "Aerodynamic" im <`Summary`>-Element enthält.  
  
-   Die **contains()** Funktion wird verwendet, um festzustellen, ob das Wort im Text enthalten ist.  
  
-   Die **value()** Methode der **Xml** -Datentyps vergleicht den Rückgabewert von **contains()** auf 1.  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. Suchen nach Produktmodellen, deren Katalogbeschreibung keine Produktmodellbilder enthält.  
 Die folgende Abfrage ruft ProductModelIDs für Produktmodelle ab, deren Katalogbeschreibungen kein <`Picture`>-Element enthalten.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Wenn die **exist()** Methode in die WHERE-Klausel False (0) zurück, die Produktmodell-ID zurückgegeben. Ansonsten wird sie nicht zurückgegeben.  
  
-   Da alle Produktbeschreibungen ein <`Picture`>-Element enthalten, ist das Resultset in diesem Fall leer.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Abfragen Einbeziehung von Hierarchien](../xquery/xqueries-involving-hierarchy.md)   
 [XQuery-Abfragen, die die Reihenfolge](../xquery/xqueries-involving-order.md)   
 [Behandlung relationaler Daten mit XQuery-Abfragen](../xquery/xqueries-handling-relational-data.md)   
 [Zeichenfolgensuche in XQuery](../xquery/string-search-in-xquery.md)   
 [Handhabung von Namespaces in XQuery](../xquery/handling-namespaces-in-xquery.md)   
 [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
