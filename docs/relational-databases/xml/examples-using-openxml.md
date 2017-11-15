---
title: 'Beispiele: Verwenden von OPENXML | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- XML [SQL Server], mapping data
- OPENXML statement, about OPENXML statement
- overflow in XML document [SQL Server]
- mapping XML data [SQL Server]
- combining attribute-centric and element centric mapping
- unconsumed data
- attribute-centric mapping
- column patterns [XML in SQL Server]
- XML [SQL Server], overflow handling
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- flags parameter
- element-centric mapping [SQL Server]
- edge tables
ms.assetid: 689297f3-adb0-4d8d-bf62-cfda26210164
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9817efb82a4b0cc7ec2beb2954b252513858064f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="examples-using-openxml"></a>Beispiele: Verwenden von OPENXML
  In den Beispielen dieses Themas wird die Verwendung von OPENXML zum Erstellen einer Rowsetansicht eines XML-Dokuments veranschaulicht. Informationen zur Syntax von OPENXML finden Sie unter [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md). Die Beispiele geben alle Aspekte von OPENXML wieder, ausgenommen der Angabe von Metaeigenschaften in OPENXML. Weitere Informationen zum Angeben von Metaeigenschaften in OPENXML finden Sie unter [Angeben von Metaeigenschaften in OPENXML](../../relational-databases/xml/specify-metaproperties-in-openxml.md).  
  
## <a name="examples"></a>Beispiele  
 Beim Abrufen der Daten wird *rowpattern* zur Identifizierung der Knoten im XML-Dokument, die die Zeilen bestimmen, verwendet. *rowpattern* wird in der XPath-Sprache ausgedrückt, die in der MSXML XPath-Implementierung verwendet wird. Wenn z. B. das Muster mit einem Element oder Attribut endet, wird eine Zeile für jeden von *rowpattern*ausgewählten Element- oder Attributknoten erstellt.  
  
 Durch den Wert des *flags* -Parameters wird die Standardzuordnung bereitgestellt. Wenn kein *ColPattern* in der *SchemaDeclaration*angegeben ist, wird die in *flags* angegebene Zuordnung verwendet. Der Wert des *flags* -Parameters wird ignoriert, wenn *ColPattern* in *SchemaDeclaration*angegeben ist. Die Angabe von *ColPattern* bestimmt den Typ der Zuordnung (attributzentriert oder elementzentriert) sowie das Verhalten im Zusammenhang mit Überlaufdaten bzw. nicht verbrauchten Daten.  
  
### <a name="a-executing-a-simple-select-statement-with-openxml"></a>A. Ausführen einer einfachen SELECT-Anweisung mit OPENXML  
 Das XML-Dokument in diesem Beispiel setzt sich aus den Elementen <`Customer`>, <`Order`> und <`OrderDetail`>zusammen. Die OPENXML-Anweisung ruft Kundeninformationen in einem zweispaltigen Rowset (**CustomerID** und **ContactName**) aus dem XML-Dokument ab.  
  
 Zunächst wird die gespeicherte Prozedur **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle zu erhalten. Dieses Dokumenthandle wird an OPENXML weitergegeben.  
  
 Die OPENXML-Anweisung verdeutlicht Folgendes:  
  
-   *rowpattern* (/ROOT/Customer) identifiziert die zu verarbeitenden <`Customer`>-Knoten.  
  
-   Der Wert des *flags*-Parameters wird auf **1** festgelegt, was die attributzentrierte Zuordnung anzeigt. Folglich werden die XML-Attribute den Spalten im Rowset, das in *SchemaDeclaration*definiert ist, zugeordnet.  
  
-   In *SchemaDeclaration*(in der WITH-Klausel) stimmen die angegebenen Werte für *ColName* mit den entsprechenden XML-Attributnamen überein. Deshalb wird der *ColPattern* -Parameter nicht in *SchemaDeclaration*angegeben.  
  
 Schließlich ruft die SELECT-Anweisung alle Spalten in dem von OPENXML bereitgestellten Rowset ab.  
  
```  
DECLARE @DocHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @DocHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@DocHandle, '/ROOT/Customer',1)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @DocHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Da die <`Customer`>-Elemente keinerlei Unterelemente besitzen, werden die Werte von **CustomerID** und **ContactName** für beide Kunden als NULL zurückgegeben, wenn dieselbe SELECT-Anweisung mit auf den Wert **2** gesetztem *flags*-Parameter ausgeführt wird, um die elementzentrierte Zuordnung anzuzeigen.  
  
 @xmlDocument kann auch vom Typ **xml** oder **(n)varchar(max)** sein.  
  
 Wenn <`CustomerID`> und <`ContactName`> im XML-Dokument Unterelemente sind, ruft die elementzentrierte Zuordnung die Werte ab.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer>  
   <CustomerID>VINET</CustomerID>  
   <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer>     
   <CustomerID>LILAS</CustomerID>  
   <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT    *  
FROM      OPENXML (@XmlDocumentHandle, '/ROOT/Customer',2)  
           WITH (CustomerID  varchar(10),  
                 ContactName varchar(20))  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Beachten Sie, dass das von **sp_xml_preparedocument** zurückgegebene Dokumenthandle für die Dauer des Batches, nicht für die Dauer der Sitzung gültig ist.  
  
### <a name="b-specifying-colpattern-for-mapping-between-rowset-columns-and-the-xml-attributes-and-elements"></a>B. Angeben von ColPattern für die Zuordnung zwischen Rowsetspalten und XML-Attributen und -Elementen  
 In diesem Beispiel wird veranschaulicht, wie das XPath-Muster im optionalen *ColPattern* -Parameter angegeben wird, um für die Zuordnung zwischen Rowsetspalten und XML-Attributen und -Elementen zu sorgen.  
  
 Das XML-Dokument in diesem Beispiel setzt sich aus den Elementen <`Customer`>, <`Order`> und <`OrderDetail`>zusammen. Die OPENXML-Anweisung ruft Kunden- und Bestellinformationen als Rowset (**CustomerID**, **OrderDate**, **ProdID** und **Qty**) aus dem XML-Dokument ab.  
  
 Zunächst wird die gespeicherte Prozedur **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle zu erhalten. Dieses Dokumenthandle wird an OPENXML weitergegeben.  
  
 Die OPENXML-Anweisung verdeutlicht Folgendes:  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail) identifiziert die zu verarbeitenden <`OrderDetail`>-Knoten.  
  
 Zur Veranschaulichung wird der Wert des *flags*-Parameters auf **2** festgelegt, was die attributzentrierte Zuordnung anzeigt. Allerdings wird diese Zuordnung durch die in *ColPattern* angegebene Zuordnung überschrieben. Das bedeutet, dass das in *ColPattern* angegebene XPath-Muster die Spalten im Rowset Attributen zuordnet. Dies führt zur attributzentrierten Zuordnung.  
  
 In *SchemaDeclaration*(in der WITH-Klausel) wird *ColPattern* auch mit den Parametern *ColName* und *ColType* angegeben. Der optionale *ColPattern* -Parameter entspricht dem angegebenen XPath-Muster und zeigt Folgendes an:  
  
-   Die **OrderID**-, **CustomerID**- und **OrderDate**-Spalten im Rowset sind den Attributen des übergeordneten Elements der von *rowpattern* identifizierten Knoten zugeordnet, und *rowpattern* identifiziert die <`OrderDetail`>-Knoten. Deshalb sind die **CustomerID**- und **OrderDate**-Spalten den **CustomerID**- und **OrderDate**-Attributen des <`Order`>-Elements zugeordnet.  
  
-   Die **ProdID** - und **Qty** -Spalten im Rowset sind den Attributen **ProductID** und **Quantity** der in *rowpattern*identifizierten Knoten zugeordnet.  
  
 Schließlich ruft die SELECT-Anweisung alle Spalten in dem von OPENXML bereitgestellten Rowset ab.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT stmt using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@XmlDocumentHandle, '/ROOT/Customer/Order/OrderDetail',2)  
WITH (OrderID     int         '../@OrderID',  
      CustomerID  varchar(10) '../@CustomerID',  
      OrderDate   datetime    '../@OrderDate',  
      ProdID      int         '@ProductID',  
      Qty         int         '@Quantity')  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
OrderID CustomerID        OrderDate          ProdID    Qty  
-------------------------------------------------------------  
10248    VINET     1996-07-04 00:00:00.000     11       12  
10248    VINET     1996-07-04 00:00:00.000     42       10  
10283    LILAS     1996-08-16 00:00:00.000     72        3  
```  
  
 Das als *ColPattern* angegebene XPath-Muster kann auch angegeben werden, um die XML-Elemente den Rowsetspalten zuzuordnen. Dies führt zur elementzentrierten Zuordnung. Im folgenden Beispiel sind die XML-Dokumentelemente <`CustomerID`> und <`OrderDate`> Unterelemente des <`Orders`>-Elements. Da *ColPattern* die im *flags* -Parameter angegebene Zuordnung überschreibt, wird der *flags* -Parameter nicht in OPENXML angegeben.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order EmployeeID="5" >  
      <OrderID>10248</OrderID>  
      <CustomerID>VINET</CustomerID>  
      <OrderDate>1996-07-04T00:00:00</OrderDate>  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order  EmployeeID="3" >  
      <OrderID>10283</OrderID>  
      <CustomerID>LILAS</CustomerID>  
      <OrderDate>1996-08-16T00:00:00</OrderDate>  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail')  
WITH (CustomerID  varchar(10)   '../CustomerID',  
      OrderDate   datetime      '../OrderDate',  
      ProdID      int           '@ProductID',  
      Qty         int           '@Quantity')  
EXEC sp_xml_removedocument @docHandle  
```  
  
### <a name="c-combining-attribute-centric-and-element-centric-mapping"></a>C. Kombinieren der attributzentrierten und der elementzentrierten Zuordnung  
 In diesem Beispiel ist der *flags* -Parameter auf den Wert **3** festgelegt und zeigt an, dass sowohl die attributzentrierte als auch die elementzentrierte Zuordnung verwendet wird. In diesem Fall wird zuerst die attributzentrierte Zuordnung und anschließend die elementzentrierte Zuordnung auf alle noch nicht verarbeiteten Spalten angewendet.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument =N'<ROOT>  
<Customer CustomerID="VINET"  >  
     <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" >   
     <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer',3)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Für **CustomerID** wird die attributzentrierte Zuordnung angewendet. Es gibt kein **ContactName**-Attribut im <`Customer`>-Element. Deshalb wird die elementzentrierte Zuordnung verwendet.  
  
### <a name="d-specifying-the-text-xpath-function-as-colpattern"></a>D. Angeben der text() XPath-Funktion als ColPattern  
 Das XML-Dokument in diesem Beispiel setzt sich aus den Elementen <`Customer`> und <`Order`> zusammen. Die OPENXML-Anweisung ruft ein Rowset ab, das sich aus dem **oid**-Attribut aus dem <`Order`>-Element, aus der ID des übergeordneten Elements des durch *rowpattern* identifizierten Knotens und aus der Blattwertzeichenfolge des Elementinhalts zusammensetzt.  
  
 Zunächst wird die gespeicherte Prozedur **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle zu erhalten. Dieses Dokumenthandle wird an OPENXML weitergegeben.  
  
 Die OPENXML-Anweisung verdeutlicht Folgendes:  
  
-   *rowpattern* (/root/Customer/Order) identifiziert die zu verarbeitenden <`Order`>-Knoten.  
  
-   Der Wert des *flags*-Parameters wird auf **1** festgelegt, was die attributzentrierte Zuordnung anzeigt. Folglich werden die XML-Attribute den in *SchemaDeclaration*definierten Rowsetspalten zugeordnet.  
  
-   In *SchemaDeclaration* (in der WITH-Klausel) stimmen die Rowsetspaltennamen **oid** und **amount** mit den entsprechenden XML-Attributnamen überein. Deshalb wird der *ColPattern* -Parameter nicht angegeben. Für die **comment** -Spalte im Rowset wird die XPath-Funktion **text()**als *ColPattern*angegeben. Dadurch wird die im *flags*-Parameter angegebene attributzentrierte Zuordnung überschrieben, und die Spalte enthält die Blattwert-Zeichenfolge des Elementinhalts.  
  
 Schließlich ruft die SELECT-Anweisung alle Spalten in dem von OPENXML bereitgestellten Rowset ab.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied  
      </Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
            <Urgency>Important</Urgency>  
            Happy Customer.  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH (oid     char(5),   
           amount  float,   
           comment ntext 'text()')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
oid   amount        comment  
----- -----------   -----------------------------  
O1    3.5           NULL  
O2    13.4          Customer was very satisfied  
O3    100.0         Happy Customer.  
O4    10000.0       NULL  
```  
  
### <a name="e-specifying-tablename-in-the-with-clause"></a>E. Angeben von TableName in der WITH-Klausel  
 In diesem Beispiel ist *TableName* in der WITH-Klausel anstelle von *SchemaDeclaration*angegeben. Dies erweist sich bei einer Tabelle, die die von Ihnen gewünschte Struktur aufweist und bei der keine Spaltenmuster ( *ColPattern* -Parameter) notwendig sind, als hilfreich.  
  
 Das XML-Dokument in diesem Beispiel setzt sich aus den Elementen <`Customer`> und <`Order`> zusammen. Die OPENXML-Anweisung ruft Bestellinformationen in einem dreispaltigen Rowset (**oid**, **date** und **amount**) aus dem XML-Dokument ab.  
  
 Zunächst wird die gespeicherte Prozedur **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle zu erhalten. Dieses Dokumenthandle wird an OPENXML weitergegeben.  
  
 Die OPENXML-Anweisung verdeutlicht Folgendes:  
  
-   *rowpattern* (/root/Customer/Order) identifiziert die zu verarbeitenden <`Order`>-Knoten.  
  
-   Die WITH-Klausel enthält *SchemaDeclaration* nicht. Anstelle dessen wird ein Tabellenname angegeben. Deshalb wird das Tabellenschema als Rowsetschema verwendet.  
  
-   Der Wert des *flags* -Parameters wird auf **1** festgelegt, was die attributzentrierte Zuordnung anzeigt. Somit werden Attribute der Elemente (identifiziert durch *rowpattern*) den Rowsetspalten mit gleichen Namen zugeordnet.  
  
 Schließlich ruft die SELECT-Anweisung alle Spalten in dem von OPENXML bereitgestellten Rowset ab.  
  
```  
-- Create a test table. This table schema is used by OPENXML as the  
-- rowset schema.  
CREATE TABLE T1(oid char(5), date datetime, amount float)  
GO  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
-- Sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH T1  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
oid   date                        amount  
----- --------------------------- ----------  
O1    1996-01-20 00:00:00.000     3.5  
O2    1997-04-30 00:00:00.000     13.4  
O3    1999-07-14 00:00:00.000     100.0  
O4    1996-01-20 00:00:00.000     10000.0  
```  
  
### <a name="f-obtaining-the-result-in-an-edge-table-format"></a>F. Ausgeben von Ergebnissen im Rahmentabellenformat  
 In diesem Beispiel wird die WITH-Klausel nicht in der OPENXML-Anweisung angegeben. Folglich weist das von OPENXML generierte Rowset ein Rahmentabellenformat auf. Die SELECT-Anweisung gibt alle Spalten in der Rahmentabelle zurück.  
  
 Das Beispiel-XML-Dokument im Beispiel setzt sich aus den Elementen <`Customer`>, <`Order`> und <`OrderDetail`>zusammen.  
  
 Zunächst wird die gespeicherte Prozedur **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle zu erhalten. Dieses Dokumenthandle wird an OPENXML weitergegeben.  
  
 Die OPENXML-Anweisung verdeutlicht Folgendes:  
  
-   *rowpattern* (/ROOT/Customer) identifiziert die zu verarbeitenden <`Customer`>-Knoten.  
  
-   Die WITH-Klausel wird nicht bereitgestellt. Deshalb gibt OPENXML das Rowset in einem Rahmentabellenformat zurück.  
  
 Schließlich gibt die SELECT-Anweisung alle Spalten in der Rahmentabelle zurück.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
SET @xmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer')  
  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Das Ergebnis wird in Form einer Rahmentabelle zurückgegeben. Informationen erhalten Sie durch Abfragen, die Sie für die Rahmentabelle schreiben. Zum Beispiel:  
  
-   Die folgende Abfrage gibt die Anzahl der **Customer** -Knoten im Dokument zurück. Da die WITH-Klausel nicht angegeben ist, gibt OPENXML eine Rahmentabelle zurück. Die SELECT-Anweisung fragt die Rahmentabelle ab.  
  
    ```  
    SELECT count(*)  
    FROM OPENXML(@docHandle, '/')  
    WHERE localname = 'Customer'  
    ```  
  
-   Die folgende Abfrage gibt die lokalen Namen der XML-Knoten vom Typ element zurück.  
  
    ```  
    SELECT distinct localname   
    FROM OPENXML(@docHandle, '/')   
    WHERE nodetype = 1   
    ORDER BY localname  
    ```  
  
### <a name="g-specifying-rowpattern-ending-with-an-attribute"></a>G. Angeben von "rowpattern", das mit einem Attribut endet  
 Das XML-Dokument in diesem Beispiel setzt sich aus den Elementen <`Customer`>, <`Order`> und <`OrderDetail`>zusammen. Die OPENXML-Anweisung ruft Bestelldetailinformationen in einem dreispaltigen Rowset (**ProductID**, **Quantity** und **OrderID**) aus dem XML-Dokument ab.  
  
 Zunächst wird **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle zu erhalten. Dieses Dokumenthandle wird an OPENXML weitergegeben.  
  
 Die OPENXML-Anweisung verdeutlicht Folgendes:  
  
-   *Rowpattern* (/ROOT/Customer/Order/OrderDetail/@ProductID) endet mit dem XML-Attribut **ProductID**. Im resultierenden Rowset wird für jeden im XML-Dokument ausgewählten Attributknoten eine Zeile erstellt.  
  
-   In diesem Beispiel wird der *flags* -Parameter nicht angegeben. Vielmehr werden die Zuordnungen vom *ColPattern* -Parameter angegeben.  
  
 In *SchemaDeclaration* (in der WITH-Klausel) wird *ColPattern* auch mit den Parametern *ColName* und *ColType* angegeben. Der optionale *ColPattern* -Parameter entspricht dem angegebenen XPath-Muster und zeigt Folgendes an:  
  
-   Das als *ColPattern* für die **ProdID**-Spalte im Rowset angegebene XPath-Muster (**.**) identifiziert den Kontextknoten (aktueller Knoten). Laut Angabe in *rowpattern* ist das das **ProductID**-Attribut des <`OrderDetail`>-Elements.  
  
-   Das für die **Qty**-Spalte im Rowset angegebene *ColPattern* **../@Quantity** identifiziert das **Quantity**-Attribut des übergeordneten Knotens (<`OrderDetail`>) des Kontextknotens (\<ProductID).  
  
-   In gleicher Weise identifiziert das für die **OID**-Spalte im Rowset angegebene *ColPattern* **../../@OrderID** das **OrderID**-Attribut des übergeordneten Knotens (<`Order`>) des Kontextknotens. Der übergeordnete Knoten ist <`OrderDetail`>, und der Kontextknoten <`ProductID`>.  
  
 Schließlich ruft die SELECT-Anweisung alle Spalten in dem von OPENXML bereitgestellten Rowset ab.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--Sample XML document  
SET @xmlDocument =N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail/@ProductID')  
       WITH ( ProdID  int '.',  
              Qty     int '../@Quantity',  
              OID     int '../../@OrderID')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Dies ist das Ergebnis:  
  
```  
ProdID      Qty         OID  
----------- ----------- -------   
11          12          10248  
42          10          10248  
72          3           10283  
```  
  
### <a name="h-specifying-an-xml-document-that-has-multiple-text-nodes"></a>H. Angeben eines XML-Dokuments mit mehreren Textknoten  
 Sind mehrere Textknoten in einem XML-Dokument vorhanden, gibt eine SELECT-Anweisung mit *ColPattern*( **text()**) nur den ersten anstelle aller Textknoten zurück. Zum Beispiel:  
  
```  
DECLARE @h int  
EXEC sp_xml_preparedocument @h OUTPUT,  
         N'<root xmlns:a="urn:1">  
           <a:Elem abar="asdf">  
             T<a>a</a>U  
           </a:Elem>  
         </root>',  
         '<ns xmlns:b="urn:1" />'  
  
SELECT * FROM openxml(@h, '/root/b:Elem')  
      WITH (Col1 varchar(20) 'text()')  
EXEC sp_xml_removedocument @h  
```  
  
 Die SELECT-Anweisung gibt **T** als Ergebnis zurück (und nicht **TaU**).  
  
### <a name="i-specifying-the-xml-data-type-in-the-with-clause"></a>I. Angeben des XML-Datentyps in der WITH-Klausel  
 In der WITH-Klausel muss ein Spaltenmuster, das der **xml** -Datentypspalte (typisiert oder nicht typisiert) zugeordnet ist, entweder eine leere Sequenz oder eine Sequenz aus Elementen, Produktionsanweisungen, Textknoten und Kommentaren zurückgeben. Die Daten werden in einen **xml** -Datentyp umgewandelt.  
  
 Im folgenden Beispiel schließt die Tabellenschemadeklaration in der WITH-Klausel **xml** -Typspalten ein.  
  
```  
DECLARE @h int  
DECLARE @x xml  
set @x = '<Root>  
  <row id="1"><lname>Duffy</lname>  
   <Address>  
            <Street>111 Maple</Street>  
            <City>Seattle</City>  
   </Address>  
  </row>  
  <row id="2"><lname>Wang</lname>  
   <Address>  
            <Street>222 Pine</Street>  
            <City>Bothell</City>  
   </Address>  
  </row>  
</Root>'  
  
EXEC sp_xml_preparedocument @h output, @x  
SELECT *  
FROM   OPENXML (@h, '/Root/row', 10)  
      WITH (id int '@id',  
  
            lname    varchar(30),  
            xmlname  xml 'lname',  
            OverFlow xml '@mp:xmltext')  
EXEC sp_xml_removedocument @h  
```  
  
 Konkret wird eine **xml**-Typvariable (@x) an die **sp_xml_preparedocument()**-Funktion übergeben.  
  
 Dies ist das Ergebnis:  
  
```  
id  lname   xmlname                   OverFlow  
--- ------- ------------------------------ -------------------------------  
1   Duffy   <lname>Duffy</lname>  <row><Address>  
                                   <Street>111 Maple</Street>  
                                   <City>Seattle</City>  
                                  </Address></row>  
2   Wang    <lname>Wang</lname>   <row><Address>  
                                    <Street>222 Pine</Street>  
                                    <City>Bothell</City>  
                                   </Address></row>  
```  
  
 Beachten Sie Folgendes im Ergebnis:  
  
-   Für die **lname**-Spalte des **varchar(30)**-Typs wird der Wert aus dem entsprechenden <`lname`>-Element abgerufen.  
  
-   Für die **xmlname** -Spalte des **xml** -Typs wird dasselbe Namenselement als Wert zurückgegeben.  
  
-   Das Flag wird auf 10 festgelegt. Der Wert 10 bedeutet "2 + 8", wobei 2 die elementzentrierte Zuordnung anzeigt und 8 anzeigt, dass nur nicht verbrauchte XML-Daten zur OverFlow-Spalte hinzugefügt werden sollen, die in der WITH-Klausel definiert ist. Wenn Sie den flags-Parameter auf den Wert 2 festlegen, wird das gesamte XML-Dokument in die OverFlow-Spalte kopiert, die in der WITH-Klausel angegeben ist.  
  
-   Falls es sich bei der Spalte in der WITH-Klausel um eine typisierte XML-Spalte handelt und die XML-Instanz nicht zum Schema passt, wird ein Fehler zurückgegeben.  
  
### <a name="j-retrieving-individual-values-from-multivalued-attributes"></a>J. Abrufen einzelner Werte aus mehrwertigen Attributen  
 Ein XML-Dokument kann mehrwertige Attribute enthalten. Das **IDREFS** -Attribut kann beispielsweise mehrwertig sein. Die Werte von mehrwertigen Attributen werden in einem XML-Dokument als Zeichenfolge angegeben, wobei die Werte durch ein Leerzeichen voneinander getrennt sind. Im folgenden XML-Dokument sind das **attends**-Attribut des \<Student>-Elements und das **attendedBy**-Attribut des \<Class>-Elements mehrwertige Attribute. Für das Abrufen einzelner Werte aus einem mehrwertigen XML-Attribut und das Speichern jedes einzelnen Wertes in einer separaten Zeile in der Datenbank ist zusätzliche Arbeit erforderlich. Dieser Vorgang wird in dem folgenden Beispiel veranschaulicht.  
  
 Dieses XML-Beispieldokument besteht aus den folgenden Elementen:  
  
-   \<Student>  
  
     Die Attribute **id** (Studenten-ID), **name**und **attends** . Das **attends** -Attribut ist ein mehrwertiges Attribut.  
  
-   \<Class>  
  
     Die Attribute **id** (Klassen-ID), **name**und **attendedBy** . Das **attendedBy** -Attribut ist ein mehrwertiges Attribut.  
  
 Das **attends**-Attribut in \<Student> und das **attendedBy**-Attribut in \<Class> stellen eine **m:n**-Beziehung zwischen den Tabellen „Student“ und „Class“ dar. Ein Student kann viele Kurse besuchen, und ein Kurs kann über viele Studenten verfügen.  
  
 Angenommen, Sie möchten dieses Dokument aufteilen und in der Datenbank wie folgt speichern:  
  
-   Speichern der \<Student>-Daten in der Students-Tabelle.  
  
-   Speichern der \<Class>-Daten in der Courses-Tabelle.  
  
-   Speichern der **m:n** -Beziehung der Daten (zwischen Student und Class) in der CourseAttendence-Tabelle. Zum Extrahieren der Werte ist zusätzliche Arbeit erforderlich. Verwenden Sie zum Abrufen dieser Informationen und Speichern in der Tabelle die folgenden gespeicherten Prozeduren:  
  
    -   **Insert_Idrefs_Values**  
  
         Fügt die Werte für die Kurs-ID und Studenten-ID in die CourseAttendence-Tabelle ein.  
  
    -   **Extract_idrefs_values**  
  
         Extrahiert die einzelnen Studenten-IDs aus jedem \<Course>-Element. Zum Abrufen dieser Werte wird eine Rahmentabelle verwendet.  
  
 Im Folgenden werden die Schritte aufgeführt:  
  
```  
-- Create these tables:  
DROP TABLE CourseAttendance  
DROP TABLE Students  
DROP TABLE Courses  
GO  
CREATE TABLE Students(  
                id   varchar(5) primary key,  
                name varchar(30)  
                )  
GO  
CREATE TABLE Courses(  
               id       varchar(5) primary key,  
               name     varchar(30),  
               taughtBy varchar(5)  
)  
GO  
CREATE TABLE CourseAttendance(  
             id         varchar(5) references Courses(id),  
             attendedBy varchar(5) references Students(id),  
             constraint CourseAttendance_PK primary key (id, attendedBy)  
)  
go  
-- Create these stored procedures:  
DROP PROCEDURE f_idrefs  
GO  
CREATE PROCEDURE f_idrefs  
    @t      varchar(500),  
    @idtab  varchar(50),  
    @id     varchar(5)  
AS  
DECLARE @sp int  
DECLARE @att varchar(5)  
SET @sp = 0  
WHILE (LEN(@t) > 0)  
BEGIN   
    SET @sp = CHARINDEX(' ', @t+ ' ')  
    SET @att = LEFT(@t, @sp-1)  
    EXEC('INSERT INTO '+@idtab+' VALUES ('''+@id+''', '''+@att+''')')  
    SET @t = SUBSTRING(@t+ ' ', @sp+1, LEN(@t)+1-@sp)  
END  
Go  
  
DROP PROCEDURE fill_idrefs  
GO  
CREATE PROCEDURE fill_idrefs   
    @xmldoc     int,  
    @xpath      varchar(100),  
    @from       varchar(50),  
    @to         varchar(50),  
    @idtable    varchar(100)  
AS  
DECLARE @t varchar(500)  
DECLARE @id varchar(5)  
  
/* Temporary Edge table */  
SELECT *   
INTO #TempEdge   
FROM OPENXML(@xmldoc, @xpath)  
  
DECLARE fillidrefs_cursor CURSOR FOR  
    SELECT CAST(iv.text AS nvarchar(200)) AS id,  
           CAST(av.text AS nvarchar(4000)) AS refs  
    FROM   #TempEdge c, #TempEdge i,  
           #TempEdge iv, #TempEdge a, #TempEdge av  
    WHERE  c.id = i.parentid  
    AND    UPPER(i.localname) = UPPER(@from)  
    AND    i.id = iv.parentid  
    AND    c.id = a.parentid  
    AND    UPPER(a.localname) = UPPER(@to)  
    AND    a.id = av.parentid  
  
OPEN fillidrefs_cursor  
FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    IF (@@FETCH_STATUS <> -2)  
    BEGIN  
        execute f_idrefs @t, @idtable, @id  
    END  
    FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
END  
CLOSE fillidrefs_cursor  
DEALLOCATE fillidrefs_cursor  
Go  
-- This is the sample document that is shredded and the data is stored in the preceding tables.  
DECLARE @h int  
EXECUTE sp_xml_preparedocument @h OUTPUT, N'<Data>  
  <Student id = "s1" name = "Student1"  attends = "c1 c3 c6"  />  
  <Student id = "s2" name = "Student2"  attends = "c2 c4" />  
  <Student id = "s3" name = "Student3"  attends = "c2 c4 c6" />  
  <Student id = "s4" name = "Student4"  attends = "c1 c3 c5" />  
  <Student id = "s5" name = "Student5"  attends = "c1 c3 c5 c6" />  
  <Student id = "s6" name = "Student6" />  
  
  <Class id = "c1" name = "Intro to Programming"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c2" name = "Databases"   
         attendedBy = "s2 s3" />  
  <Class id = "c3" name = "Operating Systems"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c4" name = "Networks" attendedBy = "s2 s3" />  
  <Class id = "c5" name = "Algorithms and Graphs"   
         attendedBy =  "s4 s5"/>  
  <Class id = "c6" name = "Power and Pragmatism"   
         attendedBy = "s1 s3 s5" />  
</Data>'  
  
INSERT INTO Students SELECT * FROM OPENXML(@h, '//Student') WITH Students  
  
INSERT INTO Courses SELECT * FROM OPENXML(@h, '//Class') WITH Courses  
/* Using the edge table */  
EXECUTE fill_idrefs @h, '//Class', 'id', 'attendedby', 'CourseAttendance'  
  
SELECT * FROM Students  
SELECT * FROM Courses  
SELECT * FROM CourseAttendance  
  
EXECUTE sp_xml_removedocument @h  
```  
  
### <a name="k-retrieving-binary-from-base64-encoded-data-in-xml"></a>K. Abrufen von Binärdaten aus Base64-codierten Daten in XML  
 Binärdaten sind häufig mithilfe der Base64-Codierung in das XML-Dokument eingeschlossen. Wenn Sie dieses XML-Dokument durch Verwenden von OPENXML aufteilen, erhalten Sie die Base64-codierten Daten. Dieses Beispiel zeigt, wie Sie die Base64-codierten Daten zurück in Binärdaten konvertieren können.  
  
-   Erstellen Sie eine Tabelle mit Beispielbinärdaten.  
  
-   Verwenden Sie eine FOR XML-Abfrage und die Option BINARY BASE64, um ein XML-Dokument zu konstruieren, in denen die Binärdaten Base64-codiert sind.  
  
-   Teilen Sie das XML-Dokument mithilfe von OPENXML auf. Die von OPENXML zurückgegebenen Daten sind Base64-codierte Daten. Rufen Sie als Nächstes die .value-Funktion auf, um sie wieder zurück in Binärdateien zu konvertieren.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 varbinary(100))  
go  
-- Insert sample binary data  
INSERT T VALUES(1, 0x1234567890)   
go  
 -- Create test XML document that has base64 encoded binary data (use FOR XML query and specify BINARY BASE64 option)  
SELECT * FROM T  
FOR XML AUTO, BINARY BASE64  
go  
-- result  
-- <T Col1="1" Col2="EjRWeJA="/>  
  
-- Now shredd the sample XML using OPENXML.   
-- Call the .value function to convert   
-- the base64 encoded data returned by OPENXML to binary.  
DECLARE @h int ;  
EXEC sp_xml_preparedocument @h OUTPUT, '<T Col1="1" Col2="EjRWeJA="/>' ;  
SELECT Col1,   
CAST('<binary>' + Col2 + '</binary>' AS XML).value('.', 'varbinary(max)') AS BinaryCol   
FROM openxml(@h, '/T')   
WITH (Col1 integer, Col2 varchar(max)) ;  
EXEC sp_xml_removedocument @h ;  
GO  
```  
  
 Dies ist das Ergebnis. Die zurückgegebenen Binärdaten sind die ursprünglichen Binärdaten in Tabelle T.  
  
```  
Col1        BinaryCol  
----------- ---------------------  
1           0x1234567890  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)   
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
