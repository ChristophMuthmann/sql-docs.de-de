---
title: FOR XML-Abfragen im Vergleich zu geschachtelten FOR XML-Abfragen | Microsoft-Dokumentation
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
- FOR XML query
- queries [XML in SQL Server], comparing query types
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2e83d836d3cf5e736847c5ebbb1934e8cde5374a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="for-xml-query-compared-to-nested-for-xml-query"></a>FOR XML-Abfragen im Vergleich zu geschachtelten FOR XML-Abfragen
  In diesem Thema wird eine einstufige FOR XML-Abfrage mit einer geschachtelten FOR XML-Abfrage verglichen. Ein Vorteil, den die Verwendung geschachtelter FOR XML-Abfragen bietet, besteht darin, dass Sie eine Kombination aus attributzentriertem und elementzentriertem XML-Code für Abfrageergebnisse angeben können. Das Beispiel veranschaulicht dies.  
  
## <a name="example"></a>Beispiel  
 Die folgende `SELECT` -Abfrage ruft Informationen zur Produktkategorie und Produktunterkategorie aus der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank ab. In der Abfrage gibt es keine geschachtelte FOR XML-Anweisung.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 Wenn Sie die `ELEMENTS` -Direktive in der Abfrage angeben, erhalten Sie ein elementzentriertes Ergebnis, wie es im folgenden Ergebnisfragment gezeigt wird:  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 Gehen wir nun davon aus, dass Sie eine XML-Hierarchie generieren möchten, die eine Kombination aus attributzentriertem und elementzentriertem XML-Code darstellt, wie das im folgenden Fragment gezeigt wird:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 Im oben gezeigten Fragment sind die Informationen zur Produktkategorie (z. B. die Kategorie-ID und der Kategoriename) Attribute. Allerdings sind die Informationen zur Unterkategorie elementzentriert. Zum Konstruieren des <`ProductCategory`>-Elements können Sie eine `FOR XML`-Abfrage wie die folgende schreiben:  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Dies ist das Ergebnis:  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 Zum Konstruieren der geschachtelten <`ProductSubCategory`>-Elemente im angestrebten XML-Code fügen Sie anschließend eine geschachtelte `FOR XML`-Abfrage hinzu, wie es im folgenden Beispiel gezeigt wird:  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Beachten Sie in der vorhergehenden Abfrage Folgendes:  
  
-   Mit der inneren `FOR XML` -Abfrage werden Informationen zur Produktunterkategorie abgerufen. Die `ELEMENTS` -Direktive wird der inneren `FOR XML` -Abfrage hinzugefügt, um elementzentrierten XML-Code zu generieren, der dem von der äußeren Abfrage generierten XML-Code hinzugefügt wird. Standardmäßig generiert die äußere Abfrage attributzentrierten XML-Code.  
  
-   In der inneren Abfrage wird die `TYPE` -Direktive angegeben, sodass das Ergebnis den **xml** -Typ aufweist. Wenn `TYPE` nicht angegeben wird, wird das Ergebnis als **nvarchar(max)** -Typ zurückgegeben, und die XML-Daten werden als Entitäten zurückgegeben.  
  
-   Die `TYPE` -Direktive wird auch in der äußeren Abfrage angegeben. Deshalb wird das Ergebnis dieser Abfrage als **xml** -Typ an den Client zurückgegeben.  
  
 Dies ist das Teilergebnis:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 Die folgende Abfrage ist lediglich eine Erweiterung der vorherigen Abfrage. Sie zeigt die vollständige Produkthierarchie in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank. Dazu gehören:  
  
-   Produktkategorien  
  
-   Produktunterkategorien in jeder Kategorie  
  
-   Produktmodelle in jeder Unterkategorie  
  
-   Produkte in jedem Produktmodell  
  
 Die folgende Abfrage kann ggf. für das Verständnis der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank nützlich sein:  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        …  
    </ProductModel>  
     …  
```  
  
 Wenn Sie die `ELEMENTS` -Direktive aus der geschachtelten `FOR XML` -Abfrage entfernen, mit der die Produktunterkategorien generiert werden, ist das gesamte Ergebnis attributzentriert. Sie können diese Abfrage dann ohne Schachtelung schreiben. Das Hinzufügen der `ELEMENTS` -Direktive ergibt einen XML-Code, der teilweise attributzentriert und teilweise elementzentriert ist. Dieses Ergebnis kann nicht durch eine FOR XML-Abfrage mit nur einer einzigen Ebene generiert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von geschachtelten FOR XML-Abfragen](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  

