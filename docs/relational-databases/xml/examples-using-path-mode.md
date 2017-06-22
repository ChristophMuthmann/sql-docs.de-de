---
title: 'Beispiele: Verwenden des PATH-Modus | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PATH FOR XML mode, examples
ms.assetid: 3564e13b-9b97-49ef-8cf9-6a78677b09a3
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 01caa2a86cde9fc2d8e857f1fd04486008d5886c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="examples-using-path-mode"></a>Beispiele: Verwenden des PATH-Modus
  Diese Beispiele veranschaulichen die Verwendung des PATH-Modus beim Generieren von XML-Code aus einer SELECT-Abfrage. Viele dieser Abfragen beziehen sich auf die XML-Dokumente mit den Fahrradfertigungsanweisungen, die in der Instructions-Spalte der ProductModel-Tabelle gespeichert sind.  
  
## <a name="specifying-a-simple-path-mode-query"></a>Angeben einer einfachen Abfrage im PATH-Modus  
 Diese Abfrage gibt einen FOR XML PATH-Modus an.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   
       ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH;  
GO  
```  
  
 Das folgende Ergebnis ist elementzentrierter XML-Code, wobei jeder Spaltenwert des resultierenden Rowsets in ein Element eingebunden wird. Da die `SELECT`-Klausel keine Aliase für die Spaltennamen angibt, sind die Namen der generierten untergeordneten Elemente mit denen der entsprechenden Spalten in der `SELECT`-Klausel identisch. Für jede Zeile des Rowsets wird ein <`row`>-Tag hinzugefügt.  
  
 `<row>`  
  
 `<ProductModelID>122</ProductModelID>`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `</row>`  
  
 `<row>`  
  
 `<ProductModelID>119</ProductModelID>`  
  
 `<Name>Bike Wash</Name>`  
  
 `</row>`  
  
 Das folgende Ergebnis ist mit dem der Abfrage im `RAW`-Modus mit angegebener Option `ELEMENTS` identisch. Es wird elementzentrierter XML-Code mit einem standardmäßigen <`row`>-Element für jede Zeile des Resultsets zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML RAW, ELEMENTS;  
```  
  
 Sie können optional angeben, dass der Name des Zeilenelements den Standard für <`row`> überschreibt. Die folgende Abfrage gibt beispielsweise das <`ProductModel`>-Element für jede Zeile des Rowsets zurück.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModel');  
GO  
```  
  
 Das XML-Ergebnis weist den angegebenen Zeilenelementnamen auf.  
  
 `<ProductModel>`  
  
 `<ProductModelID>122</ProductModelID>`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `</ProductModel>`  
  
 `<ProductModel>`  
  
 `<ProductModelID>119</ProductModelID>`  
  
 `<Name>Bike Wash</Name>`  
  
 `</ProductModel>`  
  
 Wenn Sie eine leere Zeichenfolge angeben, wird das Wrapperelement nicht erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('');  
GO  
```  
  
 Dies ist das Ergebnis:  
  
 `<ProductModelID>122</ProductModelID>`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `<ProductModelID>119</ProductModelID>`  
  
 `<Name>Bike Wash</Name>`  
  
## <a name="specifying-xpath-like-column-names"></a>Angeben von XPath-ähnlichen Spaltennamen  
 In der folgenden Abfrage beginnt der für `ProductModelID` angegebene Spaltenname mit dem @-Zeichen und enthält keinen Schrägstrich (/). Daher wird im XML-Ergebnis für das <`row`>-Element mit dem entsprechenden Spaltenwert ein Attribut erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('ProductModelData');  
GO  
```  
  
 Dies ist das Ergebnis:  
  
 `< ProductModelData id="122">`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `</ ProductModelData >`  
  
 `< ProductModelData id="119">`  
  
 `<Name>Bike Wash</Name>`  
  
 `</ ProductModelData >`  
  
 Sie können ein einzelnes Element auf höchster Ebene hinzufügen, indem Sie in `root` die Option `FOR XML`angeben.  
  
```  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 Um eine Hierarchie zu generieren, können Sie eine PATH-ähnliche Syntax einfügen. Wenn Sie beispielsweise den Spaltennamen für die `Name` -Spalte zu "SomeChild/ModelName" ändern, erhalten Sie ein hierarchisiertes XML-Ergebnis, wie im Folgenden gezeigt:  
  
 `<Root>`  
  
 `<ProductModelData id="122">`  
  
 `<SomeChild>`  
  
 `<ModelName>All-Purpose Bike Stand</ModelName>`  
  
 `</SomeChild>`  
  
 `</ProductModelData>`  
  
 `<ProductModelData id="119">`  
  
 `<SomeChild>`  
  
 `<ModelName>Bike Wash</ModelName>`  
  
 `</SomeChild>`  
  
 `</ProductModelData>`  
  
 `</Root>`  
  
 Außer der ID und dem Namen des Produktmodells ruft die folgende Abfrage die Speicherorte der Fertigungsanweisungen dieses Produktmodells ab. Da die Spalte „Instructions“ den Typ **XML** aufweist, wird die **query()** -Methode des **XML** -Datentyps angegeben, um den Speicherort abzurufen.  
  
```  
SELECT ProductModelID AS "@id",  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') AS ManuInstr  
FROM Production.ProductModel  
WHERE ProductModelID = 7  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 Dies ist das Teilergebnis. Da die Abfrage als Spaltenname „ManuInstr“ angibt, wird der von der **query()**-Methode zurückgegebene XML-Code in ein <`ManuInstr`>-Tag eingebunden, wie im Folgenden gezeigt:  
  
 `<Root>`  
  
 `<ProductModelData id="7">`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<ManuInstr>`  
  
 `<MI:Location xmlns:MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`  
  
 `<MI:step>...</MI:step>...`  
  
 `</MI:Location>`  
  
 `...`  
  
 `</ManuInstr>`  
  
 `</ProductModelData>`  
  
 `</Root>`  
  
 In die vorherige FOR XML-Abfrage können Sie eventuell für das <`Root`>- und das <`ProductModelData`>-Element Namespaces einschließen. Dies erreichen Sie, indem Sie zunächst mithilfe von WITH XMLNAMESPACES das an den Namespace zu bindende Präfix definieren und das Präfix anschließend in der FOR XML-Abfrage verwenden. Weitere Informationen finden Sie unter [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES (  
   'uri1' AS ns1,    
   'uri2' AS ns2,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' as MI)  
SELECT ProductModelID AS "ns1:ProductModelID",  
       Name           AS "ns1:Name",  
       Instructions.query('  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ('ns2:ProductInfo'), root('ns1:root');  
GO  
```  
  
 Beachten Sie, dass das `MI` -Präfix auch in `WITH XMLNAMESPACES`definiert ist. Folglich definiert die **query()** -Methode des angegebenen **XML** -Typs das Präfix nicht im Abfrageprolog. Dies ist das Ergebnis:  
  
 `<ns1:root xmlns:MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">`  
  
 `<ns2:ProductInfo>`  
  
 `<ns1:ProductModelID>7</ns1:ProductModelID>`  
  
 `<ns1:Name>HL Touring Frame</ns1:Name>`  
  
 `<MI:Location xmlns:MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`  
  
 `LaborHours="2.5" LotSize="100" MachineHours="3" SetupHours="0.5" LocationID="10" xmlns="">`  
  
 `<MI:step>`  
  
 `Insert <MI:material>aluminum sheet MS-2341</MI:material> into the <MI:tool>T-85A framing tool</MI:tool>.`  
  
 `</MI:step>`  
  
 `...`  
  
 `</MI:Location>`  
  
 `...`  
  
 `</ns2:ProductInfo>`  
  
 `</ns1:root>`  
  
## <a name="generating-a-value-list-using-path-mode"></a>Generieren einer Wertliste mithilfe des PATH-Modus  
 Diese Abfrage konstruiert für jedes Produktmodell eine Wertliste mit Produkt-IDs. Außerdem konstruiert die Abfrage für jede Produkt-ID geschachtelte <`ProductName`>-Elemente, wie im folgenden XML-Fragment gezeigt:  
  
 `<ProductModelData ProductModelID="7" ProductModelName="..."`  
  
 `ProductIDs="product id list in the product model" >`  
  
 `<ProductName>...</ProductName>`  
  
 `<ProductName>...</ProductName>`  
  
 `...`  
  
 `</ProductModelData>`  
  
 Im Folgenden wird die Abfrage gezeigt, die den gewünschten XML-Code erstellt:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID     AS "@ProductModelID",  
       Name               S "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')) S "@ProductIDs",  
       (SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
        FOR XML PATH ('')) as "ProductNames"  
FROM   Production.ProductModel  
WHERE  ProductModelID= 7 or ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Das erste geschachtelte `SELECT` gibt eine Liste von Product-IDs zurück und verwendet dabei `data()` als Spaltennamen. Da die Abfrage eine leere Zeichenfolge für den Namen des Zeilenelements in `FOR XML PATH`angibt, wird kein Element generiert. Stattdessen wird die Wertliste dem `ProductID` -Attribut zugewiesen.  
  
-   Das zweite geschachtelte `SELECT` ruft die Produktnamen der Produkte des Produktmodells auf. Es generiert <`ProductName`>-Elemente, die eingebunden in das <`ProductNames`>-Element zurückgegeben werden, da die Abfrage `ProductNames` als Spaltennamen angibt.  
  
 Dies ist das Teilergebnis:  
  
 `<ProductModelData PId="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 ...">`  
  
 `<ProductNames>`  
  
 `<ProductName>HL Touring Frame - Yellow, 60</ProductName>`  
  
 `<ProductName>HL Touring Frame - Yellow, 46</ProductName></ProductNames>`  
  
 `...`  
  
 `</ProductModelData>`  
  
 `<ProductModelData PId="9"`  
  
 `ProductModelName="LL Road Frame"`  
  
 `ProductIDs="722 723 724 ...">`  
  
 `<ProductNames>`  
  
 `<ProductName>LL Road Frame - Black, 58</ProductName>`  
  
 `<ProductName>LL Road Frame - Black, 60</ProductName>`  
  
 `<ProductName>LL Road Frame - Black, 62</ProductName>`  
  
 `...`  
  
 `</ProductNames>`  
  
 `</ProductModelData>`  
  
 Die die Produktnamen konstruierende Unterabfrage gibt das Ergebnis als Zeichenfolge zurück, die in eine Entität geändert und anschließend dem XML-Code hinzugefügt wird. Wenn Sie die TYPE-Direktive `FOR XML PATH (''), type`hinzufügen, gibt die Unterabfrage das Ergebnis als **XML** -Typ zurück, und es erfolgt keine Änderung in Entitäten.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@ProductModelID",  
      Name AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ProductIDs",  
       (  
       SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH (''), type  
       ) AS "ProductNames"  
  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
## <a name="adding-namespaces-in-the-resulting-xml"></a>Hinzufügen von Namespaces zu XML-Ergebnissen  
 Wie unter [Hinzufügen von Namespaces mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)beschrieben, können Sie WITH XMLNAMESPACES verwenden, um Namespaces in Abfragen im PATH-Modus aufzunehmen. Angenommen, die in der SELECT-Klausel angegebenen Namen enthalten Namespacepräfixe. Die folgende Abfrage im `PATH`-Modus konstruiert dieses XML-Ergebnis mit Namespaces.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
GO  
```  
  
 Das dem <`English`>-Element hinzugefügte `@xml:lang`-Attribut ist im vordefinierten XML-Namespace definiert.  
  
 Dies ist das Ergebnis:  
  
 `<Translation>`  
  
 `<English xml:lang="en">food</English>`  
  
 `<German xml:lang="ger">Essen</German>`  
  
 `</Translation>`  
  
 Die folgende Abfrage ist der in Beispiel C ähnlich, mit dem Unterschied, dass sie `WITH XMLNAMESPACES` verwendet, um Namespaces in das XML-Ergebnis einzuschließen. Weitere Informationen finden Sie unter [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES ('uri1' AS ns1,  DEFAULT 'uri2')  
SELECT ProductModelID AS "@ns1:ProductModelID",  
      Name AS "@ns1:ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ns1:ProductIDs",  
       (  
       SELECT ProductID AS "@ns1:ProductID",   
              Name AS "@ns1:ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH , type   
       ) AS "ns1:ProductNames"  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData'), root('root');  
```  
  
 Dies ist das Ergebnis:  
  
 `<root xmlns="uri2" xmlns:ns1="uri1">`  
  
 `<ProductModelData ns1:ProductModelID="7" ns1:ProductModelName="HL Touring Frame" ns1:ProductIDs="885 887 888 889 890 891 892 893">`  
  
 `<ns1:ProductNames>`  
  
 `<row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="885" ns1:ProductName="HL Touring Frame - Yellow, 60" />`  
  
 `<row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="887" ns1:ProductName="HL Touring Frame - Yellow, 46" />`  
  
 `...`  
  
 `</ns1:ProductNames>`  
  
 `</ProductModelData>`  
  
 `<ProductModelData ns1:ProductModelID="9" ns1:ProductModelName="LL Road Frame" ns1:ProductIDs="722 723 724 725 726 727 728 729 730 736 737 738">`  
  
 `<ns1:ProductNames>`  
  
 `<row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="722" ns1:ProductName="LL Road Frame - Black, 58" />`  
  
 `...`  
  
 `</ns1:ProductNames>`  
  
 `</ProductModelData>`  
  
 `</root>`  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des PATH-Modus mit FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
