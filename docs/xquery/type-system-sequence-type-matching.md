---
title: Sequenztyps | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: af693b0d47a92fdefc2ebf2104455d7ea5b782c5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="type-system---sequence-type-matching"></a>Geben Sie die System - Sequenztyps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Der Wert eines XQuery-Ausdrucks ist immer eine Sequenz aus null oder mehreren Elementen. Ein Item kann entweder ein atomarer Wert oder ein Knoten sein. Der Sequenztyp bezieht sich auf die Möglichkeit, den von einem Abfrageausdruck zurückgegebenen Sequenztyp einem bestimmten Typ zuzuordnen. Beispiel:  
  
-   Wenn der Ausdruckswert atomar ist, möchten Sie vielleicht wissen, ob er vom Typ einer ganzen Zahl (integer), einem Dezimalwert (decimal) oder einer Zeichenfolge (string) entspricht.  
  
-   Wenn der Ausdruckswert ein XML-Knoten ist, möchten Sie vielleicht wissen, ob es sich um einen Kommentarknoten, einen Verarbeitungsanweisungsknoten oder einen Textknoten handelt.  
  
-   Sie möchten vielleicht wissen, ob der Ausdruck ein XML-Element oder einen Attributknoten eines bestimmten Namens oder Typs zurückgibt.  
  
 Zur Sequenztypzuordnung können Sie den booleschen `instance of`-Operator verwenden. Weitere Informationen zu den `instance of` Ausdruck finden Sie unter [SequenceType-Ausdrücke &#40; XQuery &#41; ](../xquery/sequencetype-expressions-xquery.md).  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>Vergleichen des Typs des von einem Ausdruck zurückgegebenen atomaren Werts  
 Wenn ein Ausdruck eine Sequenz aus atomaren Werten zurückgibt, müssen Sie eventuell herausfinden, welchen Typ der Wert in der Sequenz aufweist. Die folgenden Beispiele zeigen, wie die Sequenztypsyntax verwendet werden kann, um den Typ des von einem Ausdruck zurückgegebenen atomaren Werts auszuwerten.  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>Beispiel: Ermitteln, ob eine Sequenz leer ist  
 Die **empty()** Sequence-Typs kann in einem sequenztypausdruck verwendet werden, um festzustellen, ob die Sequenz, die zurückgegeben werden, durch den angegebenen Ausdruck eine leere Sequenz ist.  
  
 Im folgenden Beispiel ermöglicht das XML-Schema, dass für das <`root`>-Element NULL-Werte zulässig sind:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 Wenn eine typisierte XML-Instanz nun einen Wert für das <`root`>-Element angibt, wird von `instance of empty()` der Wert False zurückgegeben.  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 Wenn das <`root`>-Element in der Instanz NULL-Werte enthält, stellt sein Wert eine leere Sequenz dar, und von `instance of empty()` wird der Wert True zurückgegeben.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>Beispiel: Ermitteln des Typs eines Attributwerts  
 Manchmal ist es notwendig, den von einem Ausdruck zurückgegebenen Sequenztyp vor der weiteren Verarbeitung auszuwerten. Sie können z. B. ein XML-Schema haben, in dem ein Knoten als ein union-Typ definiert ist. Im folgenden Beispiel definiert das XML-Schema in der Auflistung das Attribut `a` als einen Vereinigungstyp, dessen Wert den Datentyp decimal oder string besitzen kann.  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 Vor dem Verarbeiten einer typisierten XML-Instanz möchten Sie u. U. wissen, welchen Datentyp der Wert des Attributs `a` aufweist. Im folgenden Beispiel weist der Wert des Attributs `a` einen decimal-Datentyp auf. Aus diesem Grund`, instance of xs:decimal` gibt "true" zurück.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 Ändern Sie jetzt den Wert des Attributs `a` in einen Zeichenfolgentyp (string). `instance of xs:string` gibt den Wert True zurück.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>Beispiel: Kardinalität in Sequenzausdrücken  
 Dieses Beispiel veranschaulicht die Auswirkung einer Kardinalität in einem Sequenzausdruck. Das folgende XML-Schema definiert ein <`root`>-Element mit dem Typ Byte, für das NULL-Werte zulässig sind.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 In der folgenden Abfrage gibt `instance of` den Wert True zurück, weil der Ausdruck ein Singleton des byte-Datentyps zurückgibt.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 Wenn das <`root`>-Element gleich NULL ist, stellt sein Wert eine leere Sequenz dar. Das heißt, der Ausdruck (`/root[1]`) gibt eine leere Sequenz zurück. Deshalb gibt `instance of xs:byte` den Wert False zurück. Beachten Sie, dass die Standardkardinalität in diesem Fall 1 ist.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 Wenn Sie die Kardinalität angeben, indem Sie den Auftrittsindikator (`?`) hinzufügen, gibt der Sequenzausdruck den Wert True zurück.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 Beachten Sie, dass das Testen in einem Sequenztypausdruck in zwei Stufen erfolgt:  
  
1.  Zunächst wird beim Testen ermittelt, ob der Ausdruckstyp mit dem angegebenen Typ übereinstimmt.  
  
2.  Wenn das der Fall ist, wird anschließend ermittelt, ob die Anzahl der vom Ausdruck zurückgegebenen Items mit dem angegebenen Auftrittsindikator übereinstimmt.  
  
 Wenn beide Bedingungen erfüllt sind, gibt der `instance of`-Ausdruck den Wert True zurück.  
  
### <a name="example-querying-against-an-xml-type-column"></a>Beispiel: Abfragen einer Spalte vom Typ XML  
 Im folgenden Beispiel wird eine Abfrage angegeben, für eine Instructions-Spalte der **Xml** Geben Sie in der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank. Dies ist eine typisierte XML-Spalte, da ihr ein Schema zugeordnet ist. Das XML-Schema definiert das `LocationID`-Attribut des ganzzahligen Datentyps (integer). Aus diesem Grund im Sequenzausdruck den `instance of xs:integer?` gibt "true" zurück.  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>Vergleichen des Typs des von einem Ausdruck zurückgegebenen Knotens  
 Wenn ein Ausdruck eine Sequenz aus Knoten zurückgibt, müssen Sie eventuell herausfinden, welchen Typ der Knoten in der Sequenz aufweist. Die folgenden Beispiele zeigen, wie die Sequenztypsyntax verwendet werden kann, um den Typ des von einem Ausdruck zurückgegebenen Knotens auszuwerten. Sie können die folgenden Sequenztypen verwenden:  
  
-   **Item()** – entspricht einem beliebigen Element in der Sequenz.  
  
-   **Node()** – bestimmt, ob die Sequenz ein Knoten ist.  
  
-   **Processing-Instruction()** – bestimmt, ob der Ausdruck eine verarbeitungsanweisung zurückgibt.  
  
-   **Comment()** – bestimmt, ob der Ausdruck einen Kommentar zurückgibt.  
  
-   **Document-Node()** – bestimmt, ob der Ausdruck einen Dokumentknoten zurückgibt.  
  
 Das folgende Beispiele veranschaulicht diese Sequenztypen.  
  
### <a name="example-using-sequence-types"></a>Beispiel: Verwenden von Sequenztypen  
 In diesem Beispiel werden mehrere Abfragen für eine nicht typisierte XML-Variable ausgeführt. Diese Abfragen veranschaulichen die Verwendung der Sequenztypen.  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 In der ersten Abfrage gibt der Ausdruck den typisierten Wert des <`a`>-Elements zurück. In der zweiten Abfrage gibt der Ausdruck das <`a`>-Element zurück. Beides sind Items. Deshalb geben beide Abfragen den Wert True zurück.  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 Alle XQuery-Ausdrücke in den folgenden drei Abfragen geben das untergeordnete Element des Elementknotens für das <`root`>-Element zurück. Deshalb gibt der Sequenztypausdruck (`instance of node()`) den Wert True zurück, und die anderen beiden Ausdrücke (`instance of text()` und `instance of document-node()`) geben den Wert False zurück.  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 In der folgenden Abfrage gibt der `instance of document-node()`-Ausdruck den Wert True zurück, wenn das übergeordnete Element des <`root`>-Elements ein Dokumentknoten ist.  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 In der folgenden Abfrage ruft der Ausdruck den ersten Knoten aus der XML-Instanz ab. Da es sich dabei um einen Verarbeitungsanweisungsknoten handelt, gibt der `instance of processing-instruction()`-Ausdruck den Wert True zurück.  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Es gelten die folgenden speziellen Einschränkungen:  
  
-   **Document-Node()** mit Inhaltstyp Syntax wird nicht unterstützt.  
  
-   **Processing-Instruction(Name)** Syntax wird nicht unterstützt.  
  
## <a name="element-tests"></a>Elementtests  
 Ein Elementtest wird verwendet, um den von einem Ausdruck zurückgegebenen Elementknoten einem Elementknoten mit einem bestimmten Namen und Typ zuzuordnen. Sie können die folgenden Elementtests verwenden:  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>Attributtests  
 Der Attributtest ermittelt, ob es sich bei dem von einem Ausdruck zurückgegebenen Ausdruck um einen Attributknoten handelt. Sie können die folgenden Attributtests verwenden:  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>Testbeispiele  
 Die folgenden Beispiele veranschaulichen Szenarios, in denen Element- und Attributtests hilfreich sind.  
  
### <a name="example-a"></a>Beispiel A  
 Das folgende XML-Schema definiert den komplexen `CustomerType`; das <`firstName`>-Element und das <`lastName`>-Element sind dabei optional. Für eine angegebene XML-Instanz müssen Sie eventuell ermitteln, ob der Vorname für einen bestimmten Kunden vorhanden ist.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 Die folgende Abfrage bestimmt mit einem `instance of element (firstName)`-Ausdruck, ob das erste untergeordnete Element von <`customer`> ein Element mit dem Namen <`firstName`> ist. In diesem Fall gibt die Abfrage den Wert True zurück.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 Wenn Sie das <`firstName`>-Element aus der Instanz entfernen, wird der Wert False von der Abfrage zurückgegeben.  
  
 Sie können auch Folgendes verwenden:  
  
-   Die `element(ElementName, ElementType?)`-Sequenztypsyntax, die in der folgenden Abfrage dargestellt ist. Sie ordnet einen auf null gesetzten oder einen nicht auf null gesetzten Elementknoten zu, dessen Name `firstName` ist und dessen Typ `xs:string` ist.  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   Die `element(*, type?)`-Sequenztypsyntax, die in der folgenden Abfrage dargestellt ist. Sie ordnet den Elementknoten zu, wenn dessen Typ unabhängig von seinem Namen `xs:string` ist.  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>Beispiel B  
 Das folgende Beispiel zeigt, wie ermittelt wird, ob der von einem Ausdruck zurückgegebene Knoten ein Elementknoten mit einem bestimmten Namen ist. Er verwendet die **element()** testen.  
  
 Im folgenden Beispiel weisen die beiden abgefragten <`Customer`>-Elemente in der XML-Instanz zwei unterschiedliche Typen auf: `CustomerType` und `SpecialCustomerType`. Angenommen, Sie möchten den Typ des <`Customer`>-Elements ermitteln, das von dem Ausdruck zurückgegeben wird. Die folgende XML-Schemaauflistung definiert die Typen `CustomerType` und `SpecialCustomerType`.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 Diese XML-schemaauflistung wird verwendet, um eine typisierte erstellen **Xml** Variable. Die XML-Instanz, die dieser Variablen zugewiesen wurde, weist zwei <`customer`>-Elemente mit unterschiedlichen Typen auf. Das erste Element weist den `CustomerType`-Typ auf und das zweite Element den `SpecialCustomerType`-Typ.  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 In der folgenden Abfrage gibt der `instance of element (*, x:SpecialCustomerType ?)`-Ausdruck den Wert False zurück, weil der Ausdruck das erste Kundenelement zurückgibt, das nicht den `SpecialCustomerType`-Typ aufweist.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 Wenn Sie den Ausdruck der vorherigen Abfrage ändern und das zweite <`customer`>-Element (`/x:customer)[2]`) abrufen, gibt der `instance of`-Ausdruck den Wert <localizedText>True</localizedText> zurück.  
  
### <a name="example-c"></a>Beispiel C  
 Dieses Beispiel verwendet den Attributtest. Das folgende XML-Schema definiert den komplexen CustomerType-Typ mit den Attributen CustomerID und Age. Das Age-Attribut ist optional. Sie können für eine bestimmte XML-Instanz ermitteln, ob das Age-Attribut im <`customer`>-Element vorhanden ist.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 Die folgende Abfrage gibt den Wert True zurück, weil es in der abgefragten XML-Instanz einen Attributknoten mit dem Namen `Age` gibt. In diesem Ausdruck wird der `attribute(Age)`-Attributtest verwendet. Da Attribute keine Reihenfolge haben, verwendet die Abfrage den FLWOR-Ausdruck, um alle Attribute abzurufen, und testet dann jedes Attribut mit dem `instance of`-Ausdruck. Das Beispiel erstellt zuerst eine XML-schemaauflistung zum Erstellen einer typisierten **Xml** Variable.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 Wenn Sie das optionale `Age`-Attribut aus der Instanz entfernen, gibt die vorherige Abfrage den Wert False zurück.  
  
 Sie können im Attributtest den Attributnamen und den Attributtyp (`attribute(name,type)`) angeben.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 Alternativ können Sie angeben der `attribute(*, type)` -sequenztypsyntax. Dies ordnet den Attributknoten zu, wenn der Typ des Attributs unabhängig von dessen Namen mit dem angegebenen Typ übereinstimmt.  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Es gelten die folgenden speziellen Einschränkungen:  
  
-   Im elementtest muss der vollständigen Typnamen der auftrittsindikator folgen (**?**).  
  
-   **Element (ElementName, TypeName)** wird nicht unterstützt.  
  
-   **Element (\*, TypeName)** wird nicht unterstützt.  
  
-   **Schema-Element()** wird nicht unterstützt.  
  
-   **Schema-Attribute(AttributeName)** wird nicht unterstützt.  
  
-   Explizites Abfragen von **xsi: Type** oder **xsi: nil** wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [Typsystem &#40; XQuery &#41;](../xquery/type-system-xquery.md)  
  
  
