---
title: insert (XML DML) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: eb4082d4b14c0287571dd620021444f2ad290aa9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="insert-xml-dml"></a>insert (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fügt einen oder mehrere Knoten ein, die durch *Expression1* als unter- oder gleichgeordnete Knoten des Knotens identifiziert werden, der durch *Expression2* angegeben wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
insert   
      Expression1 (  
                 {as first | as last} into | after | before  
                                    Expression2  
                )  
```  
  
## <a name="arguments"></a>Argumente  
 *Expression1*  
 Gibt einen oder mehrere einzufügende Knoten an. Dabei kann es sich um eine konstante XML-Instanz, einen Verweis auf eine typisierte XML-Datentypinstanz der gleichen XML-Schemaauflistung, auf der die modify-Methode angewendet wird, eine nicht typisierte XML-Datentypinstanz mit einer eigenständigen **sql:column()**/**sql:variable()**-Funktion oder einen XQuery-Ausdruck handeln. Der Ausdruck kann als Ergebnis einen Knoten, einen Textknoten oder eine geordnete Sequenz von Knoten haben. Der Ausdruck kann nicht den Stammknoten (/) auflösen. Wenn das Ergebnis des Ausdrucks ein Wert oder eine Sequenz von Werten ist, werden diese Werte als einzelner Textknoten eingefügt, wobei ein Leerzeichen die einzelnen Werte in der Sequenz trennt. Wenn Sie mehrere Knoten als Konstante angeben, werden die Knoten in Klammern eingeschlossen und durch Kommas getrennt. Sie können keine heterogenen Sequenzen wie z. B. eine Sequenz aus Elementen, Attributen oder Werten einfügen. Wenn *Expression1* in eine leere Sequenz aufgelöst wird, findet kein Einfügevorgang statt, und es werden keine Fehler zurückgegeben.  
  
 into  
 Knoten, die durch *Expression1* angegeben werden, werden als direkte Nachfolger (untergeordnete Knoten) des Knotens eingefügt, der durch *Expression2* angegeben wird. Wenn der Knoten in *Expression2* bereits über einen oder mehrere untergeordnete Knoten verfügt, müssen Sie **as first** oder **as last** verwenden, wenn Sie angeben möchten, wo der neue Knoten hinzugefügt werden soll. Beispielsweise am Anfang bzw. Ende der Liste der untergeordneten Knoten. Die **as first**- und **as last**-Schlüsselwörter werden ignoriert, wenn Attribute eingefügt werden.  
  
 after  
 Knoten, die durch *Expression1* angegeben werden, werden als gleichgeordnete Knoten direkt hinter dem Knoten eingefügt, der durch *Expression2* angegeben wird. Das **after**-Schlüsselwort kann nicht zum Einfügen von Attributen verwendet werden. Es kann z. B. nicht zum Einfügen eines Attributkonstruktors oder zum Zurückgeben eines Attributs aus einer XQuery verwendet werden.  
  
 before  
 Knoten, die durch *Expression1* angegeben werden, werden als gleichgeordnete Knoten direkt vor dem Knoten eingefügt, der durch *Expression2* angegeben wird. Das **before**-Schlüsselwort kann nicht verwendet werden, wenn Attribute eingefügt werden. Es kann z. B. nicht zum Einfügen eines Attributkonstruktors oder zum Zurückgeben eines Attributs aus einer XQuery verwendet werden.  
  
 *Expression2*  
 Identifiziert einen Knoten. Die in *Expression1* identifizierten Knoten werden relativ zu dem Knoten eingefügt, der durch *Expression2* angegeben wird. Dabei kann es sich um einen XQuery-Ausdruck handeln, der einen Verweis auf einen Knoten zurückgibt, der in dem Dokument vorhanden ist, auf das aktuell verwiesen wird. Wenn mehrere Knoten zurückgegeben werden, schlägt der Einfügevorgang fehl. Wenn *Expression2* eine leere Sequenz zurückgibt, findet kein Einfügevorgang statt, und es werden keine Fehler zurückgegeben. Wenn *Expression2* keine statische SINGLETON-Instanz darstellt, wird ein statischer Fehler zurückgegeben. *Expression2* darf weder eine Verarbeitungsanweisung noch ein Kommentar oder ein Attribut sein. Beachten Sie, dass *Expression2* ein Verweis auf einen vorhandenen Knoten im Dokument, nicht auf einen erstellten Knoten, sein muss.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>A. Einfügen von Elementknoten in das Dokument  
 Das folgende Beispiel veranschaulicht das Einfügen von Elementen in ein Dokument. Zuerst wird ein XML-Dokument einer Variablen des Typs **xml** zugewiesen. Das Beispiel zeigt anschließend durch mehrere XML DML **insert**-Anweisungen, wie Elementknoten in das Dokument eingefügt werden. Nach jedem Einfügevorgang zeigt die SELECT-Anweisung das Ergebnis an.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;         
SET @myDoc = '<Root>         
    <ProductDescription ProductID="1" ProductName="Road Bike">         
        <Features>         
        </Features>         
    </ProductDescription>         
</Root>'  ;       
SELECT @myDoc;     
-- insert first feature child (no need to specify as first or as last)         
SET @myDoc.modify('         
insert <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>   
into (/Root/ProductDescription/Features)[1]') ;  
SELECT @myDoc ;        
-- insert second feature. We want this to be the first in sequence so use 'as first'         
set @myDoc.modify('         
insert <Warranty>1 year parts and labor</Warranty>          
as first         
into (/Root/ProductDescription/Features)[1]         
')  ;       
SELECT @myDoc  ;       
-- insert third feature child. This one is the last child of <Features> so use 'as last'         
SELECT @myDoc         
SET @myDoc.modify('         
insert <Material>Aluminium</Material>          
as last         
into (/Root/ProductDescription/Features)[1]         
')         
SELECT @myDoc ;        
-- Add fourth feature - this time as a sibling (and not a child)         
-- 'after' keyword is used (instead of as first or as last child)         
SELECT @myDoc  ;       
set @myDoc.modify('         
insert <BikeFrame>Strong long lasting</BikeFrame>   
after (/Root/ProductDescription/Features/Material)[1]         
')  ;       
SELECT @myDoc;  
GO  
```  
  
 Beachten Sie, dass verschiedene path-Ausdrücke in diesem Beispiel "[1]" als Anforderung für die statische Typisierung angeben. Auf diese Weise wird ein einzelner Zielknoten gewährleistet.  
  
### <a name="b-inserting-multiple-elements-into-the-document"></a>B. Einfügen von mehreren Elementen in das Dokument  
 Im folgenden Beispiel wird ein Dokument zuerst einer Variablen des Typs **xml** zugewiesen. Anschließend wird eine Sequenz aus zwei Elementen, die Produktfeatures darstellen, einer zweiten Variablen des Typs **xml** zugewiesen. Diese Sequenz wird dann in die erste Variable eingefügt.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = N'<Root>             
<ProductDescription ProductID="1" ProductName="Road Bike">             
    <Features> </Features>             
</ProductDescription>             
</Root>';  
DECLARE @newFeatures xml;  
SET @newFeatures = N'<Warranty>1 year parts and labor</Warranty>            
<Maintenance>3 year parts and labor extended maintenance is available</Maintenance>';           
-- insert new features from specified variable            
SET @myDoc.modify('             
insert sql:variable("@newFeatures")             
into (/Root/ProductDescription/Features)[1] ')             
SELECT @myDoc;  
GO  
```  
  
### <a name="c-inserting-attributes-into-a-document"></a>C. Einfügen von Attributen in ein Dokument  
 Das folgende Beispiel zeigt, wie Attribute in ein Dokument eingefügt werden. Zuerst wird ein Dokument einer Variablen des Typs **xml** zugewiesen. Anschließend wird eine Reihe von XML-DML-**insert**-Anweisungen verwendet, um Attribute in das Dokument einzufügen. Nach jeder Attributeinfügung zeigt die SELECT-Anweisung das Ergebnis an.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml ;            
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;  
SELECT @myDoc  ;          
-- insert LaborHours attribute             
SET @myDoc.modify('             
insert attribute LaborHours {".5" }             
into (/Root/Location[@LocationID=10])[1] ') ;           
SELECT @myDoc  ;          
-- insert MachineHours attribute but its value is retrived from a sql variable @Hrs             
DECLARE @Hrs float ;            
SET @Hrs =.2   ;          
SET @myDoc.modify('             
insert attribute MachineHours {sql:variable("@Hrs") }             
into   (/Root/Location[@LocationID=10])[1] ');            
SELECT @myDoc;             
-- insert sequence of attribute nodes (note the use of ',' and ()              
-- around the attributes.             
SET @myDoc.modify('             
insert (              
           attribute SetupHours {".5" },             
           attribute SomeOtherAtt {".2"}             
        )             
into (/Root/Location[@LocationID=10])[1] ');             
SELECT @myDoc;  
GO  
```  
  
### <a name="d-inserting-a-comment-node"></a>D. Einfügen eines Kommentarknotens  
 In dieser Abfrage wird ein XML-Dokument zuerst einer Variablen des Typs **xml** zugewiesen. Anschließend wird XML DML zum Einfügen eines Kommentarknotens nach dem ersten <`step`>-Element verwendet.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;           
SELECT @myDoc;             
SET @myDoc.modify('             
insert <!-- some comment -->             
after (/Root/Location[@LocationID=10]/step[1])[1] ');            
SELECT @myDoc;  
GO  
```  
  
### <a name="e-inserting-a-processing-instruction"></a>E. Einfügen einer Verarbeitungsanweisung  
 In der folgenden Abfrage wird ein XML-Dokument zuerst einer Variablen des Typs **xml** zugewiesen. Anschließend wird ein XML DML-Schlüsselwort verwendet, um eine Verarbeitungsanweisung am Anfang des Dokuments einzufügen.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>   
    <Location LocationID="10" >   
        <step>Manufacturing step 1 at this work center</step>   
        <step>Manufacturing step 2 at this work center</step>   
    </Location>   
</Root>' ;  
SELECT @myDoc ;  
SET @myDoc.modify('   
insert <?Program = "Instructions.exe" ?>   
before (/Root)[1] ') ;  
SELECT @myDoc ;  
GO  
```  
  
### <a name="f-inserting-data-using-a-cdata-section"></a>F. Einfügen von Daten mit einem CDATA-Abschnitt  
 Wenn Sie Text mit Zeichen einfügen, die in XML nicht verwendet werden können, z. B. < oder >, können Sie die Daten mithilfe von CDATA-Abschnitten einfügen, wie in der folgenden Abfrage veranschaulicht. Die Abfrage gibt einen CDATA-Abschnitt an, wird jedoch als Textknoten hinzugefügt, wobei alle ungültigen Zeichen in Entitäten konvertiert werden. '<' wird beispielsweise als &lt; gespeichert.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <ProductDescription ProductID="1" ProductName="Road Bike">             
        <Features> </Features>             
    </ProductDescription>             
</Root>' ;            
SELECT @myDoc ;            
SET @myDoc.modify('             
insert <![CDATA[ <notxml> as text </notxml> or cdata ]]>   
into  (/Root/ProductDescription/Features)[1] ') ;   
SELECT @myDoc ;  
GO  
```  
  
 Die Abfrage fügt einen Textknoten in das Element <`Features`> ein:  
  
```  
<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features> <notxml> as text </notxml> or cdata </Features>  
</ProductDescription>  
</Root>       
```  
  
### <a name="g-inserting-text-node"></a>G. Einfügen von Textknoten  
 In dieser Abfrage wird ein XML-Dokument zuerst einer Variablen des Typs **xml** zugewiesen. Im Anschluss wird mit XML DML ein Textknoten als erstes untergeordnetes Element von <`Root`> eingefügt. Der Textkonstruktor wird zum Angeben des Texts verwendet.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc;  
set @myDoc.modify('  
 insert text{"Product Catalog Description"}   
 as first into (/Root)[1]  
');  
SELECT @myDoc;  
```  
  
### <a name="h-inserting-a-new-element-into-an-untyped-xml-column"></a>H. Einfügen eines neuen Elements in eine nicht typisierte XML-Spalte  
 Das folgende Beispiel verwendet XML DML zum Aktualisieren einer XML-Instanz, die in einer Spalte vom Typ **xml** gespeichert ist:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE T (i int, x xml);  
go  
INSERT INTO T VALUES(1,'<Root>  
    <ProductDescription ProductID="1" ProductName="Road Bike">  
        <Features>  
            <Warranty>1 year parts and labor</Warranty>  
            <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
        </Features>  
    </ProductDescription>  
</Root>');  
go  
-- insert a new element  
UPDATE T  
SET x.modify('insert <Material>Aluminium</Material> as first  
  into   (/Root/ProductDescription/Features)[1]  
');  
GO  
```  
  
 Auch hier gilt: Wenn der Elementknoten <`Material`> eingefügt wird, muss vom Pfadausdruck ein einzelnes Ziel zurückgegeben werden. Dies wird explizit durch Hinzufügen des Werts [1] am Ende des Ausdrucks angegeben.  
  
```  
-- check the update  
SELECT x.query(' //ProductDescription/Features')  
FROM T;  
GO  
```  
  
### <a name="i-inserting-based-on-an-if-condition-statement"></a>I. Einfügen anhand einer Bedingungsanweisung  
 Im folgenden Beispiel wird eine IF-Bedingung als Teil von Expression1 in der XML-DML-**insert**-Anweisung angegeben. Wenn die Bedingung erfüllt ist, wird dem Element <`WorkCenter`> ein Attribut hinzugefügt.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
    <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc  
SET @myDoc.modify('  
insert  
if (/Root/Location[@LocationID=10])  
then attribute MachineHours {".5"}  
else ()  
    as first into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 Das folgende Beispiel ist ähnlich, die XML-DML-**insert**-Anweisung fügt jedoch ein Element in das Dokument ein, wenn die Bedingung den Wert True besitzt. Dies ist der Fall, wenn das Element <`WorkCenter`> nicht mehr als zwei untergeordnete <`step`>-Elemente enthält.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
        <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc;  
SET @myDoc.modify('  
insert  
if (count(/Root/Location/step) <= 2)  
then element step { "This is a new step" }  
else ()  
    as last into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Root>  
 <WorkCenter WorkCenterID="10" LaborHours="1.2">  
  <step>Manufacturing step 1 at this work center</step>  
  <step>Manufacturing step 2 at this work center</step>  
  <step>This is a new step</step>  
 </WorkCenter>  
```  
  
### <a name="j-inserting-nodes-in-a-typed-xml-column"></a>J. Einfügen von Knoten in einer typisierten XML-Spalte  
 Das folgende Beispiel fügt ein Element und ein Attribut in das XML-Dokument mit den Fertigungsanweisungen ein, das in einer typisierten **xml**-Spalte gespeichert ist.  
  
 In diesem Beispiel erstellen Sie zuerst eine Tabelle (T) mit einer typisierten **xml**-Spalte in der AdventureWorks-Datenbank. Anschließend kopieren Sie eine XML-Instanz mit Fertigungsanweisungen aus der Instructions-Spalte in der ProductModel-Tabelle in Tabelle T. Die Einfügungen werden dann am XML in Tabelle T vorgenommen.  
  
```  
USE AdventureWorks;  
GO            
DROP TABLE T;  
GO             
CREATE TABLE T(ProductModelID int primary key,    
Instructions xml (Production.ManuInstructionsSchemaCollection));  
GO  
INSERT T              
    SELECT ProductModelID, Instructions             
    FROM Production.ProductModel             
    WHERE ProductModelID=7;  
GO             
SELECT Instructions             
FROM T;  
-- now insertion begins             
--1) insert a new manu. Location. The <Root> specified as              
-- expression 2 in the insert() must be singleton.      
UPDATE T   
set Instructions.modify('   
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
insert <MI:Location LocationID="1000" >   
           <MI:step>New instructions go here</MI:step>   
         </MI:Location>   
as first   
into   (/MI:root)[1]   
') ;  
  
SELECT Instructions             
FROM T ;  
-- 2) insert attributes in the new <Location>             
UPDATE T             
SET Instructions.modify('             
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
insert attribute LaborHours { "1000" }             
into (/MI:root/MI:Location[@LocationID=1000])[1] ');   
GO             
SELECT Instructions             
FROM T ;  
GO             
--cleanup             
DROP TABLE T ;  
GO             
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;Data Modification Language&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
