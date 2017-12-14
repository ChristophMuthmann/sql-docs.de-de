---
title: "Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6730eac672d4803c3f50a200e83acb214b2986da
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] [WITH XMLNAMESPACES (Transact-SQL)](../../t-sql/xml/with-xmlnamespaces.md) bietet folgende Namespace-URI-Unterstützung:  
  
-   Macht das Namespacepräfix für die URI-Zuordnung bei Abfragen mit [Erstellen von XML mit FOR XML](../../relational-databases/xml/for-xml-sql-server.md) verfügbar.  
  
-   Macht die Namespace-URI-Zuordnung für den statischen Namespacekontext für [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)verfügbar.  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>Verwenden von WITH XMLNAMESPACES in FOR XML-Abfragen  
 Mit WITH XMLNAMESPACES können Sie XML-Namespaces in FOR XML-Abfragen einbeziehen. Nehmen Sie beispielsweise folgende FOR XML-Abfrage:  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 Dies ist das Ergebnis:  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 Um Namespaces zu dem durch die FOR XML-Abfrage erstellten XML hinzuzufügen, legen Sie zuerst mit der WITH NAMESPACES-Klausel die Zuordnungen der Namespacepräfixe zu URIs fest. Verwenden Sie anschließend in der folgenden geänderten Abfrage die Namespacepräfixe, um die in der Abfrage verwendeten Namen festzulegen. Die WITH XMLNAMESPACES-Klausel legt die Zuordnung des Namespacepräfixes (`ns1`) zum URI (`uri`) fest. Das `ns1` -Präfix wird dann beim Festlegen der Element- und Attributnamen verwendet, die durch die FOR XML-Abfrage erstellt werden sollen.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 Das XML-Ergebnis enthält die Namespacepräfixe:  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 Für die WITH XMLNAMESPACES-Klausel gilt Folgendes:  
  
-   Sie wird nur im RAW-, AUTO- und PATH-Modus der FOR XML-Abfragen unterstützt. Der EXPLICIT-Modus wird nicht unterstützt.  
  
-   Sie wirkt sich nur auf die Namespacepräfixe von FOR XML-Abfragen und auf die **xml** -Datentypmethode aus – aber nicht auf den XML-Parser. Die folgende Abfrage gibt beispielsweise einen Fehler zurück, weil das XML-Dokument keine Namespacedeklaration für das myNS-Präfix enthält.  
  
-   Die FOR XML-Direktiven XMLSCHEMA und XMLDATA können nicht zusammen mit der WITH XMLNAMESPACES-Klausel verwendet werden.  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('http://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>Verwenden der XSINIL-Direktive  
 Wenn Sie die ELEMENTS XSINIL-Direktive verwenden, können Sie das xsi-Präfix nicht in der WITH XMLNAMESPACES-Klausel definieren. Es wird stattdessen automatisch hinzugefügt, wenn Sie ELEMENTS XSINIL verwenden. Die folgende Abfrage verwendet ELEMENTS XSINIL, die elementzentriertes XML generiert, wo Elementen, deren **xsi:nil** -Attribut auf TRUE festgelegt ist, Nullwerte zugeordnet werden.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 Dies ist das Ergebnis:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>Angeben von Standardnamespaces  
 Statt ein Namespacepräfix zu deklarieren, können Sie mit dem DEFAULT-Schlüsselwort einen Standardnamespace deklarieren. In der FOR XML-Abfrage wird der Standardnamespace mit den XML-Knoten des resultierenden XML verbunden. Im folgenden Beispiel definiert WITH XMLNAMESPACES zwei Namespacepräfixe, die gemeinsam über einen Standardnamespace definiert sind.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 Die FOR XML-Abfrage generiert elementzentriertes XML. Die Abfrage verwendet bei der Knotenbenennung beide Namespacepräfixe. In der SELECT-Klausel legen ProductID, Name und Color keine Namen mit einem Präfix fest. Daher gehören die entsprechenden Elemente des resultierenden XML zum Standardnamespace.  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 Die folgende Abfrage ähnelt der vorherigen, allerdings ist der FOR XML AUTO-Modus festgelegt.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>Verwenden vordefinierter Namespaces  
 Wenn Sie vordefinierte Namespaces verwenden, müssen Sie (mit Ausnahme von xml-Namespace und xsi-Namespace, wenn ELEMENTS XSINIL verwendet wird) die Namespacebindung mit  WITH XMLNAMESPACES explizit festlegen. Die folgende Abfrage definiert explizit den Namespacepräfix für die URI-Bindung für den vordefinierten Namespace (`urn:schemas-microsoft-com:xml-sql`).  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 Dies ist das Ergebnis. SQLXML-Benutzer kennen diese XML-Vorlage. Weitere Informationen finden Sie unter [SQLXML 4.0-Programmierkonzepte](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md).  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 Nur das xml-Namespacepräfix kann verwendet werden ohne explizit in WITH XMLNAMESPACES definiert zu sein, was die folgende Abfrage im PATH-Modus zeigt. Wenn das Präfix deklariert wird, muss es außerdem mit dem Namespace http://www.w3.org/XML/1998/namespace verbunden werden. Die in der SELECT-Klausel festgelegten Namen verweisen auf das xml-Namespacepräfix, das nicht explizit mit WITH XMLNAMESPACES definiert ist.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 Die @xml:lang-Attribute verwenden den vordefinierten XML-Namespace. Da in XML Version 1.0 keine explizite Deklaration der xml-Namespacebindung notwendig ist, enthält das Ergebnis keine explizite Deklaration der Namespacebindung.  
  
 Dies ist das Ergebnis:  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>Verwenden von WITH XMLNAMESPACES mit den xml-Datentypmethoden  
 Alle in einer SELECT-Abfrage oder in UPDATE (bei der [modify()](../../t-sql/xml/xml-data-type-methods.md) -Methode) festgelegten **xml-Datentypmethoden** müssen die Namespacedeklaration in ihrem Prolog wiederholen. Dies kann einige Zeit in Anspruch nehmen. Die folgende Abfrage ruft beispielsweise Produktmodell-IDs ab, deren Katalogbeschreibungen eine Spezifikation enthalten. Dies geschieht, wenn das Element <`Specifications`> vorhanden ist.  
  
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
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 In der vorherigen Abfrage deklarieren die **query()**- und die **exist()**-Methode in ihrem Prolog denselben Namespace. Beispiel:  
  
```  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 Alternativ können Sie zuerst WITH XMLNAMESPACES deklarieren und in der Abfrage dann die Namespacepräfixe verwenden. In diesem Fall enthalten die **query()** - und die **exist()** -Methode im Prolog keine Namespacedeklaration.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 Eine explizite Deklaration im XQuery-Prolog überschreibt das in der WITH-Klausel definierte Namespacepräfix und den Standardelementnamespace.  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)   
 [WITH XMLNAMESPACES &#40;Transact-SQL&#41;](../../t-sql/xml/with-xmlnamespaces.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
