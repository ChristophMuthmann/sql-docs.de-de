---
title: Generieren eines XSD-Inlineschemas | Microsoft-Dokumentation
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
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8290d7fe8b7900291d4afe3c944564d8f2aef608
ms.lasthandoff: 04/11/2017

---
# <a name="generate-an-inline-xsd-schema"></a>Generieren eines XSD-Inlineschemas
  In einer FOR XML-Klausel können Sie anfordern, dass die Abfrage ein Inlineschema zusammen mit den Abfrageergebnissen zurückgibt. Wenn Sie ein XDR-Schema wünschen, verwenden Sie das XMLDATA-Schlüsselwort in der FOR XML-Klausel. Wenn Sie ein XSD-Schema wünschen, verwenden Sie das XMLSCHEMA-Schlüsselwort.  
  
 Dieses Thema beschreibt das XMLSCHEMA-Schlüsselwort und erläutert die Struktur des sich ergebenden XSD-Inlineschemas. Die folgenden Einschränkungen gelten beim Anfordern von Inlineschemas:  
  
-   Sie können XMLSCHEMA nur im RAW- und AUTO-Modus angeben, nicht im EXPLICIT-Modus.  
  
-   Wenn eine geschachtelte FOR XML-Abfrage die TYPE-Direktive angibt, ist das Abfrageergebnis vom Typ **xml** , und dieses Ergebnis wird als eine Instanz nicht typisierter XML-Daten behandelt. Weitere Informationen finden Sie unter [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md).  
  
 Wenn Sie XMLSCHEMA in einer FOR XML-Abfrage angeben, erhalten Sie sowohl ein Schema als auch XML-Daten als Abfrageergebnis. Jedes Datenelement der obersten Ebene verweist mithilfe einer Standard-Namespacedeklaration auf das vorherige Schema, das seinerseits auf den Zielnamespace des Inlineschemas verweist.  
  
 Beispiel:  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 Das Ergebnis enthält das XML-Schema und das XML-Ergebnis. Das <`ProductModel`>-Element der obersten Ebene im Ergebnis verweist mithilfe der Standard-Namespacedeklaration xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" auf das Schema.  
  
 Der Schemateil des Ergebnisses kann mehrere Schemadokumente enthalten, die mehrere Namespaces beschreiben. Es werden mindestens die beiden folgenden Schemadokumente zurückgegeben:  
  
-   Ein Schemadokument für den **Sqltypes** -Namespace, für das die SQL-Basistypen zurückgegeben werden.  
  
-   Ein weiteres Schemadokument, das die Form des FOR XML-Abfrageergebnisses beschreibt.  
  
 Wenn typisierte **xml** -Datentypen im Abfrageergebnis enthalten sind, werden die Schemas, die diesen typisierten **xml** -Datentypen zugeordnet sind, ebenfalls eingeschlossen.  
  
 Der Zielnamespace des Schemadokuments, das die Form des FOR XML-Ergebnisses beschreibt, enthält einen festen Teil und einen numerischen Teil, der automatisch inkrementiert wird. Das Format dieses Namespace wird im folgenden Beispiel gezeigt; dabei ist *n* eine positive ganze Zahl. In der vorherigen Abfrage ist z. B. urn:schemas-microsoft-com:sql:SqlRowSet1 der Zielnamespace.  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 Die Änderung in den Zielnamespaces, die zwischen den einzelnen Ausführungen auftritt, kann unerwünscht sein. Wenn Sie z. B. das sich ergebende XML abfragen, wird durch die Änderung im Zielnamespace ein Update der Abfrage erforderlich. Sie können optional einen Zielnamespace angeben, wenn die Option XMLSCHEMA in der FOR XML-Klausel hinzugefügt wird. Das sich ergebende XML enthält den von Ihnen bereitgestellten Namespace und bleibt unabhängig davon gleich, wie häufig die Abfrage ausgeführt wird.  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>Entitätselemente  
 Um die Einzelheiten der XSD-Schemastruktur behandeln zu können, die für das Abfrageergebnis generiert wird, muss zuerst das Entitätselement beschrieben werden.  
  
 Ein Entitätselement in den XML-Daten, die durch eine FOR XML-Abfrage zurückgegeben werden, ist ein Element, das aus einer Tabelle und nicht aus einer Spalte generiert wird. Die folgende FOR XML-Abfrage gibt z. B. Kontaktinformationen aus der `Person` -Tabelle in der `AdventureWorks2012` -Datenbank zurück.  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 Dies ist das Ergebnis:  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 In diesem Ergebnis ist <`Person`> das Entitätselement. Das XML-Ergebnis kann mehrere Entitätselemente enthalten, von denen jedes eine globale Deklaration im XSD-Inlineschema besitzt. Die folgende Abfrage ruft z. B. Bestellungskopfzeilen- und Detailinformationen für eine bestimmte Bestellung ab.  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 Da die Abfrage die ELEMENTS-Direktive angibt, ist das sich ergebende XML elementzentriert. Die Abfrage gibt außerdem die XMLSCHEMA-Direktive an. Daher wird ein XSD-Inlineschema zurückgegeben. Dies ist das Ergebnis:  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Im Ergebnis sind <`SalesOrderHeader`> und <`SalesOrderDetail`> Entitätselemente. Aus diesem Grund werden sie global im Schema deklariert. Dies bedeutet, dass die Deklaration auf der obersten Ebene im <`Schema`>-Element erfolgt.  
  
-   <`SalesOrderID`>, <`ProductID`> und <`OrderQty`> sind keine Entitätselemente, da sie Spalten zugeordnet sind. Die Spaltendaten werden aufgrund der ELEMENTS-Direktive als Elemente im XML zurückgegeben. Diese werden lokalen Elementen des complex-Typs des Entitätselements zugeordnet. Beachten Sie, dass die `SalesOrderID`-, `ProductID` - und `OrderQty` -Werte lokalen Attributen des entsprechenden complex-Typs des Entitätselements zugeordnet werden, wenn die ELEMENTS-Direktive nicht angegeben wird.  
  
## <a name="attribute-name-clashes"></a>Attributnamenkollisionen  
 Die folgende Diskussion basiert auf den Tabellen `CustOrder` und `CustOrderDetail` . Wenn Sie die folgenden Beispiele testen möchten, erstellen Sie diese Tabellen und fügen eigene Beispieldaten hinzu:  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 In FOR XML wird der gleiche Name manchmal zum Angeben verschiedener Eigenschaften oder Attribute verwendet. Die folgende attributzentrierte Abfrage im RAW-Modus generiert z. B. zwei Attribute, die den gleichen Namen (OrderID) besitzen. In diesem Fall wird ein Fehler generiert.  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 Da es jedoch zulässig ist, zwei Elemente mit gleichem Namen zu verwenden, können Sie das Problem durch Hinzufügen der ELEMENTS-Direktive beseitigen:  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 Dies ist das Ergebnis. Beachten Sie, dass das OrderID-Element im XSD-Inlineschema zweimal definiert wird. In einer der Deklarationen wird minOccurs entsprechend der OrderID aus der CustOrderDetail-Tabelle auf 0 festgelegt, in der zweiten Deklaration erfolgt die Zuordnung zur primären Schlüsselspalte OrderID der `CustOrder` -Tabelle, wobei minOccurs standardmäßig den Wert 1 besitzt.  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>Elementnamenkollisionen  
 In FOR XML kann der gleiche Name zum Angeben von zwei Unterelementen verwendet werden. Die folgende Abfrage ruft z. B. die ListPrice- und DealerPrice-Werte von Produkten ab; die Abfrage gibt jedoch den gleichen Alias (Price) für diese beiden Spalten an. Aus diesem Grund besitzt das sich ergebende Rowset zwei Spalten mit dem gleichen Namen.  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>Fall 1: Beide Unterelemente sind Nichtschlüsselspalten des gleichen Typs und können den Wert NULL besitzen  
 In der folgenden Abfrage sind beide Unterelemente Nichtschlüsselspalten des gleichen Typs und können den Wert NULL besitzen.  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Dies ist das entsprechende XML, das generiert wird. Es wird nur ein Teil des XSD-Inlineschemas dargestellt.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 Beachten Sie Folgendes bezüglich des XSD-Inlineschemas:  
  
-   ListPrice und DealerPrice sind vom gleichen Datentyp (`money`), und beide Angaben können in der Tabelle den Wert NULL aufweisen. Da sie im sich ergebenden XML nicht zurückgegeben werden können, ist nur ein untergeordnetes <`Price`>-Element in der komplexen Typdeklaration des <`row`>-Elements vorhanden, das die Werte "minOccurs=0" und "maxOccurs=2" aufweist.  
  
-   Da der Wert `DealerPrice` in der Tabelle NULL ist, wird nur `ListPrice` als <`Price`>-Element zurückgegeben. Wenn Sie der ELEMENTS-Direktive den `XSINIL`-Parameter hinzufügen, erhalten Sie beide Elemente, deren Wert `xsi:nil`für das <`Price`>-Element auf TRUE festgelegt wurde, das DealerPrice entspricht. Außerdem erhalten Sie zwei untergeordnete <`Price`>-Elemente in der komplexen Typdefinition <`row`> im XSD-Inlineschema, wobei das `nillable`-Attribut für beide auf TRUE festgelegt wurde. Dieses Fragment ist ein Teilergebnis:  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>Fall 2: Eine Schlüssel- und eine Nichtschlüsselspalte des gleichen Typs  
 Die folgende Abfrage zeigt eine Schlüssel- und eine Nichtschlüsselspalte des gleichen Typs.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 Die folgende Abfrage für die Tabelle **T** gibt den gleichen Alias für Col1 und Col2 an, wobei Col1 ein Primärschlüssel ist und nicht null sein darf, wohingegen Col2 null sein darf. Diese Abfrage generiert zwei gleichgeordnete Elemente, die untergeordnete Elemente des <`row`>-Elements sind.  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Dies ist das Ergebnis. Es wird nur ein Fragment des XSD-Schemas dargestellt.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 Beachten Sie im XSD-Inlineschema, dass für das <`Col`>-Element, das Col2 entspricht, minOccurs auf 0 festgelegt wurde.  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>Fall 3: Beide Elemente eines unterschiedlichen Typs und entsprechender Spalten dürfen NULL sein  
 Die folgende Abfrage wird für die gleiche Tabelle angegeben, die auch in Fall 2 gezeigt wurde:  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 In der folgenden Abfrage erhalten Col2 und Col3 den gleichen Alias. Diese Abfrage generiert zwei gleichgeordnete Elemente, die den gleichen Namen besitzen und untergeordnete Elemente des <`raw`>-Elements im Ergebnis sind. Diese beiden Spalten gehören unterschiedlichen Typen an und dürfen NULL sein Dies ist das Ergebnis. Es wird nur ein Teil des XSD-Inlineschemas gezeigt.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 Beachten Sie Folgendes bezüglich des XSD-Inlineschemas:  
  
-   Da sowohl Col2 als auch Col3 NULL sein dürfen, gibt die Deklaration des <`Col`>-Elements minOccurs als 0 und maxOccurs als 2 an.  
  
-   Da beide <`Col`>-Elemente gleichgeordnete Elemente sind, ist im Schema eine Elementdeklaration vorhanden. Da die Elemente unterschiedlichen Typen angehören, obwohl beide Elemente simple-Typen sind, ist der Typ des Elements im Schema `xsd:anySimpleType`. Im Ergebnis wird jeder Instanztyp durch das `xsi:type`-Attribut identifiziert.  
  
-   Im Ergebnis verweist jede Instanz des <`Col`>-Elements mithilfe des `xsi:type`-Attributs auf ihren Instanztyp.  
  
  
