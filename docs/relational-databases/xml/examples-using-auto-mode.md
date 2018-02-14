---
title: 'Beispiele: Verwenden des AUTO-Modus | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: edb1a03183a36c6308b2b7d14253179ac52d9494
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="examples-using-auto-mode"></a>Beispiele: Verwenden des AUTO-Modus
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Die folgenden Beispiele veranschaulichen die Verwendung des AUTO-Modus. Viele dieser Abfragen beziehen sich auf die XML-Dokumente mit den Fahrradproduktionsanweisungen, die in der Instructions-Spalte der ProductModel-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Beispieldatenbank gespeichert sind.  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>Beispiel: Abrufen von Kunden-, Bestell- und Bestelldetailinformationen  
 Mit dieser Abfrage werden die Kunden-, Bestell- und Bestelldetailinformationen für einen bestimmten Kunden abgerufen.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 Da die Abfrage Tabellenaliasnamen für `Cust`, `OrderHeader`, `Detail`und `Product` identifiziert, werden durch den `AUTO` -Modus die entsprechenden Elemente generiert. Auch hier gilt: Durch die Reihenfolge, in der die Tabellen durch die in der `SELECT` -Klausel angegebenen Spalten identifiziert werden, wird die Hierarchie dieser Elemente ermittelt.  
  
 Dies ist das Teilergebnis.  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>Beispiel: Angeben von GROUP BY- und Aggregatfunktionen  
 Die folgende Abfrage gibt individuelle Kunden-IDs sowie die Anzahl der Bestellungen zurück, die der Kunde jeweils angefordert hat.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>Beispiel: Angeben von berechneten Spalten im AUTO-Modus  
 Diese Abfrage gibt verkettete Namen einzelner Kunden sowie die Bestellinformationen zurück. Das liegt daran, dass die berechnete Spalte der innersten Ebene zugeordnet ist, die an dieser Stelle entdeckt wird, was in diesem Beispiel das <`SOH`>-Element ist. Die verketteten Kundennamen werden als Attribute des <`SOH`>-Elements dem Resultset hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 Um die <`IndividualCustomer`>-Elemente abzurufen, die das `Name`-Attribut besitzen, das die Kopfzeileninformationen zu jeder Bestellung als ein Unterelement enthält, wird die Abfrage mithilfe eines untergeordneten SELECT-Ausdrucks umgeschrieben. Der innere SELECT-Ausdruck erstellt eine temporäre `IndividualCustomer`-Tabelle mit der berechneten Spalte, die die Namen der einzelnen Kunden enthält. Diese Tabelle wird anschließend mit der `SalesOrderHeader` -Tabelle verknüpft, um das Resultset zu erzielen.  
  
 Beachten Sie, dass die `Sales.Customer` -Tabelle individuelle Kundeninformationen speichert, wozu auch der `PersonID` -Wert für den Kunden gehört. Diese `PersonID` wird dann zum Suchen des Kontaktnamens in der `Person.Person` -Tabelle verwendet.  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 Dies ist das Teilergebnis:  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>Beispiel: Zurückgeben von Binärdaten  
 Diese Abfrage gibt ein Produktfoto aus der Tabelle `ProductPhoto` zurück. `ThumbNailPhoto` ist eine **varbinary (max)** -Spalte in der `ProductPhoto` -Tabelle. Der `AUTO` -Modus gibt standardmäßig einen Verweis (eine relative URL auf das virtuelle Stammverzeichnis der Datenbank, in der die Abfrage ausgeführt wird) auf die Binärdaten zurück. Das `ProductPhotoID` -Schlüsselattribut muss angegeben werden, damit das Bild später identifiziert werden kann. Beim Abrufen eines Bildverweises wie in diesem Beispiel muss der Primärschlüssel der Tabelle ebenfalls in der `SELECT` -Klausel angegeben werden, damit eine Zeile eindeutig identifiziert wird.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 Dies ist das Ergebnis:  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 Die gleiche Abfrage wird mit der Option `BINARY BASE64` ausgeführt. Die Abfrage gibt die Binärdaten im Base64-codierten Format zurück.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 Dies ist das Ergebnis:  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 Standardmäßig wird beim Verwenden des AUTO-Modus zum Abrufen von Binärdaten statt der Binärdaten ein Verweis (eine relative URL auf das virtuelle Stammverzeichnis der Datenbank, in der die Abfrage ausgeführt wurde) zurückgegeben. Das geschieht, wenn die Option BINARY BASE64 nicht angegeben wurde.  
  
 Wenn der AUTO-Modus einen URL-Verweis auf die Binärdaten in Datenbanken zurückgibt, die die Groß-/Kleinschreibung nicht berücksichtigen, und wenn der in der Abfrage angegebene Tabellen- oder Spaltenname nicht mit dem Tabellen- oder Spaltennamen in der Datenbank übereinstimmt, wird die Abfrage ausgeführt. Allerdings ist dann die im Verweis zurückgegebene Groß-/Kleinschreibung nicht konsistent. Zum Beispiel:  
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 Dies ist das Ergebnis:  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 Das kann insbesondere dann ein Problem darstellen, wenn dbobject-Abfragen für eine Datenbank mit Unterscheidung zwischen Groß- und Kleinschreibung ausgeführt werden. Um dieses Problem zu vermeiden, sollte die Groß-/Kleinschreibung des in Abfragen angegebenen Tabellen- oder Spaltennamens mit der Groß-/Kleinschreibung des Tabellen- oder Spaltennamens in der Datenbank übereinstimmen.  
  
## <a name="example-understanding-the-encoding"></a>Beispiel: Grundlegendes zur Codierung  
 Dieses Beispiel zeigt mehrere Codierungen, die in dem Resultset auftreten.  
  
 Erstellen Sie die folgende Tabelle:  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 Fügen Sie die folgenden Daten zu der Tabelle hinzu:  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 Diese Abfrage gibt die Daten aus der Tabelle zurück. Der FOR XML AUTO-Modus ist angegeben. Binärdaten werden als Verweis zurückgegeben.  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 Dies ist das Ergebnis:  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 Dies ist der Vorgang für die Codierung von Sonderzeichen in dem Ergebnis:  
  
-   Im Abfrageergebnis werden die in den Element- und Attributnamen zurückgegebenen XML- und URL-Sonderzeichen codiert, indem der hexadezimale Wert des entsprechenden Unicode-Zeichens verwendet wird. Im vorherigen Beispiel wird der Elementname <`Special Chars`> als <`Special_x0020_Chars`> zurückgegeben. Der Attributname <`Col#&2`> wird als <`Col_x0023__x0026_2`> zurückgegeben. Sowohl XML- als auch URL-Sonderzeichen werden codiert.  
  
-   Falls die Werte der Elemente oder Attribute einen der fünf standardmäßigen XML-Zeichenentitäten (', "", \<, > und &) enthalten, werden diese XML-Sonderzeichen immer mithilfe der XML-Zeichencodierung codiert. Im vorherigen Resultset wird der Wert `&` im Wert des Attributs <`Col1`> als `&` codiert. Das #-Zeichen bleibt jedoch unverändert, da es sich hierbei um ein gültiges XML-Zeichen und kein XML-Sonderzeichen handelt.  
  
-   Falls die Werte der Elemente oder Attribute ein URL-Sonderzeichen enthalten, das in der URL eine besondere Bedeutung hat, werden sie nur im DBOBJECT URL-Wert codiert. Dies geschieht nur, wenn das Sonderzeichen Teil eines Tabellen- oder Spaltennamens ist. Im Resultset wird das `#` -Zeichen, das Teil des Tabellennamens `Col#&2` ist, als `_x0023_ in the DBOJBECT URL`codiert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden des AUTO-Modus mit FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
