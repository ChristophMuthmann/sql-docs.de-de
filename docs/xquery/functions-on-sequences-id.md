---
title: ID-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 963e5eb2c2b0ddaec5674f2f7c5f930ed6c34806
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-sequences---id"></a>Funktionen für Sequenzen - Id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Sequenz der Elementknoten mit xs: ID-Werte, die die Werte aus einem oder mehreren der xs: IDREF-Werte, die im angegebenen entsprechen *$arg*.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Ein oder mehrere xs:IDREF-Werte.  
  
## <a name="remarks"></a>Hinweise  
 Das Ergebnis der Funktion ist eine Sequenz von Elementen in der XML-Instanz in der Dokumentreihenfolge, die einen xs:ID-Wert gleich einem oder mehreren xs:IDREF-Werten in der Liste der xs:IDREF-Kandidaten besitzt.  
  
 Wenn der xs:IDREF-Wert keinem Element entspricht, gibt die Funktion die leere Sequenz zurück.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** in Spalten vom Typ der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. Abrufen von Elementen anhand des Werts des IDREF-Attributs  
 Im folgenden Beispiel werden die <`employee`>-Elemente mit fn:id anhand des IDREF-Managerattributs abgerufen. In diesem Beispiel ist das Manager-Attribut ein Attribut vom Typ IDREF, und das eid-Attribut ist ein Attribut vom Typ ID.  
  
 Für einen bestimmten Manager-Attributwert der **id()** -Funktion sucht die <`employee`>-Element, dessen ID-Attributwert Typ, den IDREF-Eingabewert übereinstimmt. Das heißt, für einen bestimmten Mitarbeiter die **id()** idatabasebackupreadstream Mitarbeiter-Manager.  
  
 Im Beispiel geschieht Folgendes:  
  
-   Es wird eine XML-Schemaauflistung erstellt.  
  
-   Eine typisierte **Xml** Variable wird mithilfe der XML-schemaauflistung erstellt.  
  
-   Die Abfrage ruft das Element mit dem ID-Attributwert verweist die **Manager** IDREF-Attribut von der <`employee`> Element.  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 Die Abfrage gibt "Dave" als Wert zurück. Dies gibt an, dass Dave Joes Manager ist.  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. Abrufen von Elementen anhand des Werts des IDREFS-Attributs von OrderList  
 Im folgenden Beispiel ist das OrderList-Attribut des <`Customer`>-Elements ein Attribut vom Typ IDREFS. Es listet die Bestellungs-IDs für diesen bestimmten Kunden auf. Für jede order_id ist ein untergeordnetes <`Order`>-Element unter dem <`Customer`> mit dem entsprechenden Wert vorhanden.  
  
 Der Abfrageausdruck `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` ruft den ersten Wert aus der IDRES-Liste für den ersten Kunden ab. Dieser Wert wird dann zum Übergeben der **id()** Funktion. Die Funktion sucht dann nach den <`Order`>-Element, dessen OrderID-Attributwert, die Eingabe für übereinstimmt, die **id()** Funktion.  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]unterstützt nicht die Version der zwei Argumente des **id()**.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Der Argumenttyp von erfordert **id()** einen Untertyp von xs: IDREF * sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen für Sequenzen](http://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  

