---
title: OPENXML (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs:
- TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f5b32c99393bb5b7f31423df840f7f0069dd3518
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OPENXML stellt eine Rowsetsicht eines XML-Dokuments bereit. Da OPENXML ein Rowsetanbieter ist, kann OPENXML in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen überall dort verwendet werden, wo Rowsetanbieter, wie z. B. eine Tabelle, eine Sicht oder die OPENROWSET-Funktion, verwendet werden können.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>Argumente  
 *idoc*  
 Das Dokumenthandle für die interne Darstellung eines XML-Dokuments. Die interne Darstellung eines XML-Dokuments wird durch Aufrufen von **sp_xml_preparedocument** erstellt.  
  
 *rowpattern*  
 Das XPath-Muster, das zum Identifizieren der Knoten (im XML-Dokument, dessen Handle im *idoc*-Parameter übergeben wird) verwendet wird, die als Zeilen verarbeitet werden sollen.  
  
 *flags*  
 Gibt die zwischen den XML-Daten und dem relationalen Rowset zu verwendende Zuordnung an und legt fest, wie die Überlaufspalte ausgefüllt wird. *flags* ist ein optionaler Eingabeparameter, wobei folgende Werte möglich sind.  
  
|Bytewert|Description|  
|----------------|-----------------|  
|**0**|**Attributzentrierte** Zuordnung als Standard verwenden.|  
|**1**|Verwenden der **attributzentrierten** Zuordnung. Kann mit XML_ELEMENTS kombiniert werden. In diesem Fall wird zuerst die **attributzentrierte** Zuordnung und anschließend die **elementzentrierte** Zuordnung auf alle noch nicht verarbeiteten Spalten angewendet.|  
|**2**|Verwenden der **elementzentrierten** Zuordnung. Kann mit XML_ATTRIBUTES kombiniert werden. In diesem Fall wird zuerst die **attributzentrierte** Zuordnung und anschließend die **elementzentrierte** Zuordnung auf alle noch nicht verarbeiteten Spalten angewendet.|  
|**8**|Kann mit XML_ATTRIBUTES oder XML_ELEMENTS kombiniert werden (logisches OR). Im Kontext des Abrufens zeigt dieses Flag an, dass die verwendeten Daten nicht in die Überlaufeigenschaft **@mp:xmltext** kopiert werden sollen.|  
  
 *SchemaDeclaration*  
 Die Schemadefinition im folgenden Format: *ColName**ColType* [*ColPattern* | *MetaProperty*] [**,***ColNameColType* [*ColPattern* | *MetaProperty*]...]  
  
 *ColName*  
 Der Name einer Spalte des Rowsets.  
  
 *ColType*  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp der Spalte des Rowsets. Wenn der Spaltentyp vom zugrunde liegenden **xml**-Datentyp des Attributs abweicht, tritt eine erzwungene Typkoersion auf.  
  
 *ColPattern*  
 Ein optionales allgemeines XPath-Muster, das beschreibt, wie die XML-Knoten den Spalten zugeordnet werden sollten. Wenn *ColPattern* nicht angegeben ist, wird die Standardzuordnung (**attributzentrierte** oder **elementzentrierte** Zuordnung, wie von *flags* angegeben) verwendet.  
  
 Das als *ColPattern* angegebene XPath-Muster wird zum Angeben der besonderen Eigenheit der Zuordnung (im Fall der **attributzentrierten** und **elementzentrierten** Zuordnung) verwendet, die die von *flags* angegebene Standardzuordnung überschreibt oder erweitert.  
  
 Das allgemeine, als *ColPattern* angegebene XPath-Muster unterstützt auch die Metaeigenschaften.  
  
 *MetaProperty*  
 Eine der von OPENXML bereitgestellten Metaeigenschaften. Wenn *MetaProperty* angegeben ist, enthält die Spalte von der Metaeigenschaft bereitgestellte Informationen. Die Metaeigenschaften ermöglichen es Ihnen, Informationen (wie etwa die relative Position oder Namespaceinformationen) über XML-Knoten zu extrahieren. Dies bietet mehr Informationen, als in der Textdarstellung zu sehen sind.  
  
 *TableName*  
 Der Tabellenname, der (anstelle von *SchemaDeclaration*) angegeben werden kann, wenn bereits eine Tabelle mit dem gewünschten Schema vorhanden ist und keine Spaltenmuster erforderlich sind.  
  
## <a name="remarks"></a>Remarks  
 Die WITH-Klausel stellt ein Rowsetformat bereit (und bei Bedarf auch zusätzliche Zuordnungsinformationen) und verwendet dazu *SchemaDeclaration* oder die Angabe eines vorhandenen Tabellennamens (*TableName*). Wenn die optionale WITH-Klausel nicht angegeben ist, werden die Ergebnisse in einem Rahmentabellenformat (**edge**) zurückgegeben. Rahmentabellen geben die differenzierte XML-Dokumentstruktur (z. B. Element-/Attributnamen, die Dokumenthierarchie, Namespaces, Verarbeitungsanweisungen usw.) in einer einzelnen Tabelle wieder.  
  
 In der folgenden Tabelle wird die Struktur der Rahmentabelle (**edge**) beschrieben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|Die eindeutige ID des Dokumentknotens.<br /><br /> Das Stammelement hat den ID-Wert 0. Die negativen ID-Werte sind reserviert.|  
|**parentid**|**bigint**|Identifiziert das übergeordnete Element des Knotens. Das durch diese ID identifizierte übergeordnete Element ist nicht notwendigerweise das übergeordnete Element; dies hängt vielmehr vom Knotentyp (NodeType) des Knotens ab, dessen übergeordnetes Element nicht von dieser ID identifiziert wird. Wenn es sich bei dem Knoten beispielsweise um einen Textknoten handelt, kann das übergeordnete Objekt ein Attributknoten sein.<br /><br /> Wenn sich der Knoten auf der obersten Ebene im XML-Dokument befindet, ist **ParentID** gleich NULL.|  
|**nodetype**|**int**|Identifiziert den Knotentyp. Eine ganze Zahl, die der XML DOM-Knotentypnummer (Document Object Model) entspricht.<br /><br /> Die Knotentypen sind Folgende:<br /><br /> 1 = Elementknoten<br /><br /> 2 = Attributknoten<br /><br /> 3 = Textknoten|  
|**localname**|**nvarchar**|Gibt den lokalen Namen des Elements oder Attributs an. Ist NULL, wenn das DOM-Objekt keinen Namen hat.|  
|**Präfix**|**nvarchar**|Das Namespacepräfix des Knotennamens.|  
|**namespaceuri**|**nvarchar**|Der Namespace-URI (Universal Resource Identifier) des Knotens. Ist der Wert NULL, ist kein Namespace vorhanden.|  
|**datatype**|**nvarchar**|Der eigentliche Datentyp der Element- oder Attributzeile, der andernfalls NULL ist. Der Datentyp wird aus der Inline-DTD (Document Type Definition) oder aus dem Inlineschema abgeleitet.|  
|**prev**|**bigint**|Die XML-ID des vorhergehenden gleichgeordneten Elements. Ist NULL, wenn kein direktes vorhergehendes gleichgeordnetes Element vorhanden ist.|  
|**text**|**ntext**|Enthält den Attributwert oder den Elementinhalt in Textform (oder ist NULL, wenn der Rahmentabelleneintrag (**edge**) keinen Wert benötigt).|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. Verwenden einer einfachen SELECT-Anweisung mit OPENXML  
 Im folgenden Beispiel wird eine interne Darstellung eines XML-Images mithilfe von `sp_xml_preparedocument` erstellt. Es wird dann eine `SELECT`-Anweisung, die einen `OPENXML`-Rowsetanbieter verwendet, für die interne Darstellung des XML-Dokuments ausgeführt.  
  
 Der *flag*-Wert wird auf `1` festgelegt. Dies zeigt die Verwendung der **attributzentrierten** Zuordnung an. Daher werden die XML-Attribute den Spalten im Rowset zugeordnet. Mit *rowpattern*, das als `/ROOT/Customer` angegeben ist, werden die zu verarbeitenden `<Customers>`-Knoten identifiziert.  
  
 Der optionale *ColPattern*-Parameter (Spaltenmuster) wird nicht angegeben, da der Spaltenname mit den XML-Attributnamen übereinstimmt.  
  
 Der `OPENXML`-Rowsetanbieter erstellt ein zweispaltiges Rowset (`CustomerID` und `ContactName`), aus dem die `SELECT`-Anweisung die benötigten Spalten abruft (in diesem Fall alle Spalten).  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Wenn dieselbe `SELECT`-Anweisung mit dem Wert `2` für *flags* ausgeführt wird, wodurch die **elementzentrierte** Zuordnung angezeigt wird, werden die Werte von `CustomerID` und `ContactName` für beide Kunden im XML-Dokument als NULL zurückgegeben, da das XML-Dokument keine Elemente mit dem Namen `CustomerID` oder `ContactName` enthält.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. Angeben von ColPattern für die Zuordnung zwischen Spalten und den XML-Attributen  
 Die folgende Abfrage gibt die Attribute für die Kunden-ID, das Bestelldatum, die Produkt-ID und die Menge aus dem XML-Dokument zurück. *rowpattern* identifiziert die `<OrderDetails>`-Elemente. `ProductID` und `Quantity` sind die Attribute des `<OrderDetails>`-Elements. `OrderID`, `CustomerID` und `OrderDate` sind jedoch die Attribute des übergeordneten Elements (`<Orders>`).  
  
 Der optionale *ColPattern*-Wert wird angegeben. Dies zeigt Folgendes an:  
  
-   Die Spalten `OrderID`, `CustomerID` und `OrderDate` des Rowsets werden den Attributen des übergeordneten Knotens der Knoten zugeordnet, die von *rowpattern* im XML-Dokument identifiziert werden.  
  
-   Die `ProdID`-Spalte des Rowsets wird dem `ProductID`-Attribut und die `Qty`-Spalte des Rowsets wird dem `Quantity`-Attribut der Knoten zugeordnet, die in *rowpattern* identifiziert sind.  
  
 Zwar ist durch den *flags*-Parameter die **elementzentrierte** Zuordnung angegeben, die im *ColPattern*-Parameter angegebene Zuordnung überschreibt jedoch diese Zuordnung.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',   
               CustomerID  varchar(10) '../@CustomerID',   
               OrderDate   datetime    '../@OrderDate',   
               ProdID      int         '@ProductID',   
               Qty         int         '@Quantity');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. Abrufen von Ergebnissen in einem Rahmentabellenformat  
 Das XML-Dokument in diesem Beispiel setzt sich aus den Elementen `<Customers>`, `<Orders>` und `<Order_0020_Details>` zusammen. Zunächst wird **sp_xml_preparedocument** aufgerufen, um ein Dokumenthandle abzurufen. Dieses Dokumenthandle wird an `OPENXML` übergeben.  
  
 In der `OPENXML`-Anweisung identifiziert *rowpattern* (`/ROOT/Customers`) die zu verarbeitenden `<Customers>`-Knoten. Da die WITH-Klausel nicht angegeben ist, wird das Rowset von `OPENXML` in einem Rahmentabellenformat (**edge**) zurückgegeben.  
  
 Schließlich ruft die `SELECT`-Anweisung alle Spalten in der Rahmentabelle (**edge**) ab.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Beispiele: Verwenden von OPENXML](../../relational-databases/xml/examples-using-openxml.md)  
  
  
