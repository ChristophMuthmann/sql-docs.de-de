---
title: EXIST()-Methode (Xml-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e152abc34c459d82f451c5ded02d30f5fb76b23
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="exist-method-xml-data-type"></a>exist()-Methode (XML-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt ein **Bit** mit folgenden Bedeutungen zurück:  
  
-   1 bedeutet True, wenn der XQuery-Ausdruck in einer Abfrage ein nicht leeres Ergebnis zurückgibt, d. h. wenn er mindestens einen XML-Knoten zurückgibt.  
  
-   0 bedeutet False, wenn er ein leeres Ergebnis zurückgibt.  
  
-   NULL, wenn die Instanz vom Datentyp **xml** , für die die Abfrage ausgeführt wurde, NULL enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>Argumente  
 XQuery  
 Ein XQuery-Ausdruck, ein Zeichenfolgenliteral.  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]  
>  Die **exist()** -Methode gibt 1 für den XQuery-Ausdruck zurück, der ein nicht leeres Ergebnis zurückgibt. Wenn Sie die **true()** - oder **false()** -Funktionen in der **exist()** -Methode angeben, gibt die **exist()** -Methode 1 zurück, da die Funktionen **true()** und **false()** den booleschen Wert True bzw. False zurückgeben. D. h., sie geben ein nicht leeres Ergebnis zurück. Daher gibt **exist()** den Wert 1 (True) zurück, wie im folgenden Beispiel gezeigt:  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen wird veranschaulicht, wie die **exist()** -Methode angegeben wird.  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>Beispiel: Angeben der exist()-Methode für eine Variable vom Typ xml  
 Im folgenden Beispiel @x ist ein **Xml** Typvariablen (nicht typisiertes Xml) und @f ist eine Ganzzahlvariable für den Typ, der den Rückgabewert von speichert die **exist()** Methode. Die **exist()** -Methode gibt True zurück (1), wenn der in der XML-Instanz gespeicherte Datumswert `2002-01-01`ist.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 Beachten Sie beim Vergleichen von Datumswerten mit der **exist()** -Methode Folgendes:  
  
-   Zum Vergleichen der Werte wird der Code `cast as xs:date?` verwendet, um die Werte in Werte vom Typ **xs:date** umzuwandeln.  
  
-   Der Wert, der die  **@Somedate**  -Attributs ist nicht typisiert. Beim Vergleichen wird der Wert implizit in den Typ auf der rechten Seite des Vergleichs, den **xs:date** -Datentyp, umgewandelt.  
  
-   Anstelle von **cast as xs:date()**können Sie die **xs:date()** -Konstruktorfunktion verwenden. Weitere Informationen finden Sie unter [Konstruktorfunktionen &#40; XQuery &#41; ](../../xquery/constructor-functions-xquery.md).  
  
 Im folgende Beispiel ähnelt der vorherigen Abfrage, außer dass es wurde eine <`Somedate`> Element.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **text()** -Methode gibt einen Textknoten zurück, der den nicht typisierten Wert `2002-01-01`enthält (Der XQuery-Typ ist **xdt: UntypedAtomic**.) Sie müssen explizit umwandeln dieser typisierten Wert von **x** auf **xsd: Date**, da das implizite Umwandeln in diesem Fall nicht unterstützt wird.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>Beispiel: Angeben der exist()-Methode für eine typisierte xml-Variable  
 Das folgende Beispiel veranschaulicht die Verwendung der **exist()** -Methode für eine Variable vom Typ **xml** . Es handelt sich hier um eine typisierte XML-Variable, da sie den Namen des Namespace der Schemaauflistung angibt: `ManuInstructionsSchemaCollection`.  
  
 Im Beispiel mit den fertigungsanweisungen Dokument zuerst diese Variablen zugewiesen und dann die **exist()** Methode dient zum Ermitteln, ob das Dokument enthält ein <`Location`> Element, dessen **LocationID**  Attributwert lautet "50".  
  
 Die **exist()** Methode, die auf die mit der @x Variable gibt 1 (True) zurück, wenn die produktionsanweisungen Dokument enthält ein <`Location`> Element mit `LocationID=50`. Anderenfalls gibt sie 0 (False) zurück.  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>Beispiel: Angeben der exist()-Methode für eine Spalte vom Typ xml  
 Die folgende Abfrage ruft Produktmodell-IDs, deren katalogbeschreibungen nicht die Spezifikationen enthalten <`Specifications`> Element:  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die WHERE-Klausel wählt nur diejenigen Zeilen aus der **ProductDescription** -Tabelle aus, die die für die **CatalogDescription** -Spalte vom Typ XML angegebene Bedingung erfüllen.  
  
-   Die **exist()** Methode in die WHERE-Klausel 1 (True) zurück, wenn der XML-Code nicht einschließt <`Specifications`> Element. Beachten Sie die Verwendung der [NOT()-Funktion (XQuery)](../../xquery/functions-on-boolean-values-not-function.md).  
  
-   Die [SQL:Column()-Funktion (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) Funktion wird verwendet, um den Wert aus einer nicht-XML-Spalte zu importieren.  
  
-   Diese Abfrage gibt ein leeres Rowset zurück.  
  
 Die Abfrage gibt die **query()** - und die **exist()** -Methode vom XML-Datentyp an. Beide Methoden deklarieren denselben Namespace im Abfrageprolog. In diesem Fall bietet es sich an, WITH XMLNAMESPACES zu verwenden, um das Präfix zu deklarieren und in der Abfrage zu verwenden.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

