---
title: SequenceType-Ausdrücke (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 86b5cbc103e79fa06a30321b27ff26c3d55b818c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sequencetype-expressions-xquery"></a>SequenceType-Ausdrücke (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In XQuery ist jeder Wert eine Sequenz. Der Typ des Werts wird als Sequenztyp bezeichnet. Der Sequenztyp kann verwendet werden, eine **Instanz** XQuery-Ausdruck. Die in der XQuery-Spezifikation beschriebene SequenceType-Syntax wird verwendet, wenn in einem XQuery-Ausdruck auf einen Typ verwiesen werden muss.  
  
 Der atomare Typname kann auch verwendet werden, der **umgewandelt als** XQuery-Ausdruck. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **Instanz** und **umgewandelt als** XQuery-Ausdrücke für Sequenztypen teilweise unterstützt werden.  
  
## <a name="instance-of-operator"></a>instance of-Operator  
 Die **Instanz** -Operator kann verwendet werden, um den dynamischen oder zur Laufzeit den Typ des Werts des angegebenen Ausdrucks zu bestimmen. Beispiel:  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 Beachten Sie, dass die `instance of` -Operator, der `Occurrence indicator`, gibt die Kardinalität, Anzahl der Elemente in der resultierenden Sequenz. Wenn dieser Operator nicht angegeben wird, wird eine Kardinalität von 1 verwendet. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], nur das Fragezeichen (**?)**  häufigkeitsindikator unterstützt. Die **?** -häufigkeitsindikator zeigt an, dass `Expression` kann NULL oder ein Element(e) zurückgeben. Wenn die **?** -häufigkeitsindikator angegeben ist, `instance of` gibt true zurück, wenn die `Expression` Typ entspricht dem angegebenen `SequenceType`, unabhängig davon, ob `Expression` gibt ein Singleton oder eine leere Sequenz zurück.  
  
 Wenn die **?** -häufigkeitsindikator nicht angegeben ist, `sequence of` gibt "true" nur, wenn die `Expression` Übereinstimmungen geben die `Type` angegebenen und `Expression` ein Singleton zurückgibt.  
  
 **Hinweis** das Pluszeichen (**+**) und das Sternchen (**\***) häufigkeitsindikatoren können nicht [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Die folgenden Beispiele veranschaulichen die Verwendung der**Instanz** -Operators in XQuery.  
  
### <a name="example-a"></a>Beispiel A  
 Das folgende Beispiel erstellt eine **Xml** Variablen vom Typ und gibt eine Abfrage dafür an. Der Abfrageausdruck gibt einen `instance of`-Operator an, um zu bestimmen, ob der dynamische Typ des von dem ersten Operanden zurückgegebenen Werts mit dem im zweiten Operanden angegebenen Typ übereinstimmt.  
  
 Die folgende Abfrage gibt "true", da der Wert 125 eine Instanz des angegebenen Typs ist **xs: Integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 Die folgende Abfrage gibt True zurück, da der von dem Ausdruck (/a[1]) zurückgegebene Wert im ersten Operanden ein Element ist:  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 Entsprechend gibt `instance of` in der folgenden Abfrage True zurück, da der Werttyp des Ausdrucks im ersten Ausdruck ein Attribut ist:  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 Im folgenden Beispiel gibt der Ausdruck `data(/a[1]` einen atomaren Wert mit der Typisierung xdt:untypedAtomic zurück. Folglich gibt `instance of` TRUE zurück.  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 In der folgenden Abfrage gibt der Ausdruck `data(/a[1]/@attrA` einen nicht typisierten atomaren Wert zurück. Folglich gibt `instance of` TRUE zurück.  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>Beispiel B  
 In diesem Beispiel fragen Sie eine typisierte XML-Spalte in der AdventureWorks-Beispieldatenbank ab. Die der abzufragenden Spalte zugeordnete XML-Schemaauflistung stellt die Typisierungsinformationen bereit.  
  
 Im Ausdruck **data()** gibt den typisierten Wert des ProductModelID-Attributs, dessen Typ xs: String, gemäß dem Schema der Spalte zugeordnet. Folglich gibt `instance of` TRUE zurück.  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 Die folgenden Abfragen UsetheBoolean `instance of` Ausdrucks zum bestimmen, ob das LocationID-Attribut vom Typ xs: Integer ist:  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Die folgende Abfrage wird für die typisierte CatalogDescription-Spalte vom Typ XML angegeben. Die dieser Spalte zugeordnete XML-Schemaauflistung stellt die Typisierungsinformationen bereit.  
  
 Die Abfrage verwendet den `element(ElementName, ElementType?)`-Test im `instance of`-Ausdruck, um zu überprüfen, ob `/PD:ProductDescription[1]` einen Elementknoten eines bestimmten Namens und Typs zurückgibt.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 Diese Abfrage gibt True zurück.  
  
### <a name="example-c"></a>Beispiel C  
 Beim Verwenden von UNION-Datentypen in einem `instance of`-Ausdruck gilt in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die folgende Einschränkung: speziell wenn ein Element oder Attribut vom Typ UNION ist, kann `instance of` den genauen Typ möglicherweise nicht bestimmen. Folglich gibt eine Abfrage False zurück, es sei denn, der in SequenceType verwendete atomare Typ ist das höchste übergeordnete Element des aktuellen Typs des Ausdrucks in der simpleType-Hierarchie. Mit anderen Worten müssen die in SequenceType angegebenen atomaren Typen dem Typ anySimpleType direkt untergeordnet sein. Informationen zu der Typhierarchie finden Sie unter [Typumwandlungsregeln in XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 Das nächste Abfragebeispiel führt folgende Vorgänge aus:  
  
-   Erstellen einer XML-Schemaauflistung und Definieren eines UNION-Typs wie integer oder string.  
  
-   Deklarieren einer typisierten **Xml** -Variablen mithilfe der XML-schemaauflistung.  
  
-   Zuordnen einer XML-Beispielinstanz zu der Variablen.  
  
-   Abfragen der Variablen, um das Verhalten von `instance of` mit einem UNION-Typ zu veranschaulichen.  
  
 Im Folgenden wird die Abfrage aufgeführt:  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 Die folgende Abfrage gibt False zurück, da der in dem `instance of`-Ausdruck angegebene Sequenztyp nicht das höchste übergeordnete Element des aktuellen Typs des angegebenen Ausdrucks ist. Das heißt, der Wert von <`TestElement`> ist ein ganzzahliger Typ. das höchste übergeordnete Element ist xs:decimal. Es ist jedoch nicht als der zweite Operand des `instance of`-Operators angegeben.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 Nachdem das höchste übergeordnete Element von xs:integer xs:decimal ist, würde die Abfrage True zurückgeben, wenn Sie sie ändern und xs:decimal als SequenceType angeben.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>Beispiel D  
 In diesem Beispiel Sie zunächst eine XML-schemaauflistung erstellen und verwenden, um Geben Sie eine **Xml** Variable. Das typisierte **Xml** Variable wird dann abgefragt, um zu veranschaulichen die `instance of` Funktionalität.  
  
 Die folgende XML-Schemaauflistung definiert den einfachen Typ myType sowie das Element <`root`> vom gleichen Typ:  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 Erstellen Sie nun eine typisierte **Xml** Variable und sie abzufragen:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 Nachdem der myType-Typ durch Einschränkung aus einem im sqltpypes-Schema definierten varchar-Typ abgeleitet ist, gibt `instance of` ebenfalls True zurück.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>Beispiel E  
 Im folgenden Beispiel ruft der Ausdruck einen der Werte des IDREFS-Attributs auf und verwendet `instance of`, um zu bestimmen, ob der Wert vom Typ IDREF ist. Das Beispiel führt die folgenden Aktionen aus:  
  
-   Erstellt eine XML-schemaauflistung in der die <`Customer`>-Element verfügt über ein **OrderList** Attribut vom Typ IDREFS, und die <`Order`>-Element verfügt über ein **OrderID** ID-Attributtyp.  
  
-   Erstellt eine typisierte **Xml** -Variable und weist dieser eine XML-Beispielinstanz zu.  
  
-   Gibt eine Abfrage für die Variable an. Der Abfrageausdruck ruft den ersten Wert für die Bestell-ID vom OrderList-Attribut des Typs IDRERS für den ersten <`Customer`> ab. Der abgerufene Wert ist vom Typ IDREF. Folglich gibt `instance of` True zurück.  
  
```  
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
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **schema-element()** und **schema-attribute()** Sequenztypen werden nicht unterstützt, für den Vergleich mit der `instance of` Operator.  
  
-   Vollständige Sequenzen wie z. B. `(1,2) instance of xs:integer*` werden nicht unterstützt.  
  
-   Wenn Sie eine Form der verwenden die **element()** -Sequenztyp, der angibt, wie z. B. einen Typnamen `element(ElementName, TypeName)`, der Typ muss mit einem Fragezeichen (?) qualifiziert werden. `element(Title, xs:string?)` gibt beispielsweise an, dass für das Element NULL-Werte zulässig sind. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt keine Erkennung zur Laufzeit von der **xsi: nil** Eigenschaft mithilfe von `instance of`.  
  
-   Wenn der Wert in `Expression` aus einem als UNION typisierten Element oder Attribut stammt, identifiziert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nur den Grundtyp, nicht aber den Typ, aus dem der Typ des Werts abgeleitet wurde. Wenn <`e1`> beispielsweise mit dem statischen Typ (xs:integer | xs:string) definiert wurde, gibt Folgendes den Wert False zurück.  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     Jedoch gibt `data(<e1>123</e1>) instance of xs:decimal` True zurück.  
  
-   Für die **processing-instruction()** und **document-node()** -Sequenztyp sind nur Formen ohne Argumente sind zulässig. Beispielsweise `processing-instruction()` ist zulässig, aber `processing-instruction('abc')` ist nicht zulässig.  
  
## <a name="cast-as-operator"></a>cast as-Operator  
 Die **umgewandelt als** Ausdruck kann verwendet werden, um einen Wert in einen bestimmten Datentyp konvertieren. Beispiel:  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ist das Fragezeichen (?) nach `AtomicType` erforderlich. Z. B. in der folgenden Abfrage gezeigt `"2" cast as xs:integer?` konvertiert den Zeichenfolgenwert in eine ganze Zahl:  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 In der folgenden Abfrage **data()** gibt den typisierten Wert des ProductModelID-Attributs, ein String-Datentyp zurück. Die `cast as`-Operator konvertiert den Wert zu xs: Integer.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Die explizite Verwendung der **data()** in dieser Abfrage nicht erforderlich ist. Der `cast as`-Ausdruck führt die implizite Atomisierung des Eingabeausdrucks aus.  
  
### <a name="constructor-functions"></a>Konstruktorfunktionen  
 Sie können die Konstruktorfunktionen für atomare Typen verwenden. Beispielsweise anstelle der `cast as` Operator `"2" cast as xs:integer?`, können Sie die **Xs:integer()** Konstruktorfunktion, wie im folgenden Beispiel:  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 Das folgende Beispiel gibt einen Datumswert vom Typ xs:date gleich 2000-01-01Z zurück.  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 Sie können Konstruktoren auch für benutzerdefinierte atomare Typen verwenden. Wenn die XML-schemaauflistung zugeordnet definiert der XML-Datentyp z. B. einen einfachen Typ, eine **myType()** Konstruktor kann verwendet werden, um einen Wert dieses Typs zurückzugeben.  
  
#### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
  
-   Die XQuery-Ausdrücke **Typeswitch**, **umwandelbare**, und **behandeln** werden nicht unterstützt.  
  
-   **umgewandelt als** erfordert ein Fragezeichen (?) nach dem atomaren Typ.  
  
-   **xs: QName** wird als Typ für die Umwandlung von Typen nicht unterstützt. Verwendung **expanded-QName** stattdessen.  
  
-   **xs: Date**, **xs: Time**, und **xs: DateTime** erfordern eine Zeitzone, die durch ein Z gekennzeichnet ist.  
  
     Die folgende Abfrage schlägt fehl, da die Zeitzone nicht angegeben ist.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     Wenn Sie dem Wert ein Z zum Anzeigen der Zeitzone hinzufügen, kann die Abfrage ordnungsgemäß ausgeführt werden.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     Dies ist das Ergebnis:  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Ausdrücke](../xquery/xquery-expressions.md)   
 [Typsystem &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
