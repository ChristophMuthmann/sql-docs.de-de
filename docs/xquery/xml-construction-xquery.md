---
title: XML-Konstruktion (XQuery) | Microsoft Docs
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
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 542ab45094806cd59c6f80038e38b73c1efa338f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="xml-construction-xquery"></a>XML-Konstruktion (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In XQuery können Sie die **direkte** und **berechnet** Konstruktoren zum Erstellen von XML-Strukturen in einer Abfrage.  
  
> [!NOTE]  
>  Besteht kein Unterschied zwischen der **direkte** und **berechnet** Konstruktoren.  
  
## <a name="using-direct-constructors"></a>Verwenden von direkten Konstruktoren  
 Wenn Sie direkte Konstruktoren verwenden, geben Sie beim Konstruieren des XML-Codes eine XML-ähnliche Syntax an. Die folgenden Beispiele veranschaulichen die XML-Konstruktion mit direkten Konstruktoren.  
  
### <a name="constructing-elements"></a>Konstruktion von Elementen  
 Sie können Elemente konstruieren, indem Sie die XML-Schreibweise verwenden. Im folgenden Beispiel wird die direkter Konstruktor als Ausdruck verwendet und erstellt eine \<ProductModel >-Element. Das konstruierte Element besitzt drei untergeordnete Elemente.  
  
-   Einen Textknoten.  
  
-   Zwei Elementknoten, \<Zusammenfassung > und \<Funktionen >.  
  
    -   Die \<Summary >-Element verfügt über einen untergeordneten Textknoten, dessen Wert ist "Some Description".  
  
    -   Die \<Features >-Element verfügt über drei untergeordnete Elementknoten, \<Color >, \<Gewichtung >, und \<Garantie >. Jeder dieser Knoten besitzt einen weiteren untergeordneten Textknoten mit den Werten Red, 25 und 2 years parts and labor.  
  
```  
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 Dies ist das XML-Ergebnis:  
  
```  
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 Wie in diesem Beispiel gezeigt, erweist sich das Konstruieren von Elementen aus konstanten Ausdrücken zwar als nützlich; die wahre Stärke dieser Funktion der XQuery-Sprache liegt jedoch in der Möglichkeit, XML-Code zu konstruieren, mit dem Daten dynamisch aus einer Datenbank extrahiert werden können. Verwenden Sie zum Angeben von Abfrageausdrücken geschweifte Klammern. Im XML-Ergebnis wird der Ausdruck dann durch seinen Wert ersetzt. Die folgende Abfrage konstruiert beispielsweise ein <`NewRoot`>-Element mit einem untergeordneten <`e`>-Element. Der Wert des Elements <`e`> wird berechnet, indem Sie die Angabe eines pfadausdrucks in geschweiften Klammern ("{... }").  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 Die geschweiften Klammern fungieren als Token, die einen Kontextwechsel bewirken, sodass die Abfrage von der XML-Konstruktion zur Abfrageauswertung wechselt. In diesem Fall wird der XQuery-Pfadausdruck innerhalb der geschweiften Klammern (`/root`) ausgewertet und durch sein Ergebnis ersetzt.  
  
 Dies ist das Ergebnis:  
  
```  
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 Die folgende Abfrage ist der vorherigen ähnlich, Allerdings gibt der Ausdruck in der geschweiften Klammern der **data()** -Funktion zum Abrufen von des atomaren Wert, der die <`root`> Element und weist sie auf das konstruierte Element <`e`>.  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 Dies ist das Ergebnis:  
  
```  
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 Wenn die geschweiften Klammern Teil Ihres Texts sein sollen, d. h. nicht als Kontextwechseltoken fungieren sollen, können Sie als Escapezeichen "}}" und "{{" verwenden, wie im folgenden Beispiel gezeigt:  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 Dies ist das Ergebnis:  
  
```  
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 Die folgende Abfrage ist ein weiteres Beispiel für die Konstruktion von Elementen mithilfe des direkten Elementkonstruktors. Dabei wird der Wert des <`FirstLocation`>-Elements durch Ausführen des Ausdrucks in geschweiften Klammern erhalten. Der Abfrageausdruck gibt die Fertigungsschritte am ersten Arbeitsplatzstandort aus der Instructions-Spalte der Production.ProductModel-Tabelle zurück.  
  
```  
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Dies ist das Ergebnis:  
  
```  
<FirstLocation>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>Elementinhalt in der XML-Konstruktion  
 Das folgende Beispiel veranschaulicht das Verhalten von Ausdrücken beim Konstruieren von Elementinhalten mithilfe des direkten Konstruktors. Im folgenden Beispiel gibt der direkte Elementkonstruktor einen Ausdruck an. Für diesen Ausdruck wird im daraus resultierenden XML-Code ein Textknoten erstellt.  
  
```  
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 Die aus der Auswertung des Ausdrucks resultierende Sequenz atomarer Werte wird dem Textknoten hinzugefügt, wobei die einzelnen atomaren Werte durch Leerzeichen getrennt werden, wie im Ergebnis gezeigt. Das konstruierte Element besitzt ein untergeordnetes Element. Es handelt sich um einen Textknoten, der den im Ergebnis gezeigten Wert enthält.  
  
```  
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 Wenn Sie anstelle eines einzigen Ausdrucks drei verschiedene Ausdrücke angeben, die drei Textknoten generieren, werden die aneinander angrenzenden Textknoten im XML-Ergebnis durch Verkettung zu einem einzigen zusammengeführt.  
  
```  
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 Der konstruierte Elementknoten besitzt ein untergeordnetes Element. Es handelt sich um einen Textknoten, der den im Ergebnis gezeigten Wert enthält.  
  
```  
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>Konstruktion von Attributen  
 Beim Konstruieren von Elementen mithilfe des direkten Elementkonstruktors können Sie über eine XML-ähnliche Syntax Elementattribute angeben, wie im folgenden Beispiel gezeigt:  
  
```  
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 Dies ist das XML-Ergebnis:  
  
```  
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 Das erstellte Element <`ProductModel`> besitzt ein ProductModelID-Attribut und folgende untergeordnete Knoten:  
  
-   Einen Textknoten, `This is product model catalog description.`.  
  
-   Einen Elementknoten, <`Summary`>. Dieser Knoten besitzt einen untergeordneten Textknoten, `Some description`.  
  
 Beim Konstruieren eines Attributs können Sie dessen Wert durch einen Ausdruck in geschweiften Klammern angeben. In diesem Fall wird das Ergebnis des Ausdrucks als der Attributwert zurückgegeben.  
  
 Im folgenden Beispiel die **data()** Funktion ist nicht zwingend erforderlich. Da Sie ein Attribut den Wert des Ausdrucks zuweisen **data()** implizit angewendet, um den typisierten Wert des angegebenen Ausdrucks abzurufen.  
  
```  
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 Dies ist das Ergebnis:  
  
```  
<NewRoot attr="5" />  
```  
  
 Es folgt eine weiteres Beispiel, in dem Ausdrücke für die Konstruktion der LocationID- und SetupHrs-Attribute angegeben werden. Diese Ausdrücke werden für den XML-Code in der Instructions-Spalte ausgewertet. Der typisierte Wert des Ausdrucks wird anschließend den Attributen zugewiesen.  
  
```  
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step …   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Mehrere oder gemischte Attributausdrücke (d. h. Zeichenfolgen- und XQuery-Ausdrücke) werden nicht unterstützt. Wie in der folgenden Abfrage gezeigt, konstruieren Sie beispielsweise XML-Code, in dem `Item` eine Konstante ist, und der Wert `5` durch Auswerten eines Abfrageausdrucks erhalten wird:  
  
    ```  
    <a attr="Item 5" />  
    ```  
  
     Die folgende Abfrage gibt einen Fehler zurück, da Sie eine Zeichenfolgenkonstante mit einem Ausdruck ({/x}) verwendet haben und dies nicht unterstützt wird:  
  
    ```  
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     In diesem Fall haben Sie folgende Möglichkeiten:  
  
    -   Sie können den Attributwert durch Verkettung zweier atomarer Werte bilden. Diese atomaren Werte werden für den Attributwert serialisiert, wobei zwischen die beiden Werte ein Leerzeichen eingefügt wird:  
  
        ```  
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         Dies ist das Ergebnis:  
  
        ```  
        <a attr="Item 5" />  
        ```  
  
    -   Verwenden der [Concat-Funktion](../xquery/functions-on-string-values-concat.md) um zwei Zeichenfolgenargumente in der resultierenden Attributwert zu verketten:  
  
        ```  
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         In diesem Fall wird zwischen den beiden Zeichenfolgenwerten kein Leerzeichen eingefügt. Wenn Sie die beiden Werte doch durch ein Leerzeichen trennen möchten, müssen Sie dies explizit angeben.  
  
         Dies ist das Ergebnis:  
  
        ```  
        <a attr="Item5" />  
        ```  
  
-   Mehrere Ausdrücke werden als Attributwert nicht unterstützt. So gibt beispielsweise folgende Abfrage einen Fehler zurück:  
  
    ```  
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   Heterogene Sequenzen werden nicht unterstützt. Der Versuch, eine heterogene Sequenz als Attributwert zuzuweisen, gibt einen Fehler zurück, wie im folgenden Beispiel gezeigt. In diesem Beispiel wird eine heterogene Sequenz, nämlich die Zeichenfolge "Item" und ein Element <`x`> als Attributwert angegeben:  
  
    ```  
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     Wenden Sie die **data()** -Funktion, die Abfrage funktioniert, da er ruft den atomaren Wert des Ausdrucks ab `/x`, die mit der Zeichenfolge verkettet wird. Es folgt eine Sequenz atomarer Werte:  
  
    ```  
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     Dies ist das Ergebnis:  
  
    ```  
    <a attr="Item 5" />  
    ```  
  
-   Die Reihenfolge der Attributknoten wird während der Serialisierung erzwungen und nicht während der Überprüfung des statischen Typs. Beispielsweise ist die folgende Abfrage fehlerhaft, weil sie versucht, nach einem Nichtattributknoten einen Attributknoten hinzuzufügen.  
  
    ```  
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     Die obige Abfrage gibt den folgenden Fehler zurück:  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>Hinzufügen von Namespaces  
 Beim Konstruieren von XML-Code mithilfe von direkten Konstruktoren können die konstruierten Element- und Attributnamen durch das Verwenden von Namespacepräfixen qualifiziert werden. Es gibt folgende Möglichkeiten, um Präfixe an Namespaces zu binden:  
  
-   Mithilfe eines Namespacedeklarationsattributs.  
  
-   Mithilfe der WITH XMLNAMESPACES-Klausel.  
  
-   Im XQuery-Prolog.  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>Verwenden eines Namespacedeklarationsattributs zum Hinzufügen von Namespaces  
 Im folgenden Beispiel wird ein Namespacedeklarationsattribut in der Konstruktion des <`a`>-Elements verwendet, um einen Standardnamespace zu deklarieren. Durch die Konstruktion des untergeordneten <`b`>-Elements wird die Deklaration des Standardnamespace im übergeordneten Element rückgängig gemacht.  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 Dies ist das Ergebnis:  
  
```  
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 Sie können dem Namespace ein Präfix zuweisen. Das Präfix wird in der Konstruktion des <`a`>-Elements angegeben.  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 Dies ist das Ergebnis:  
  
```  
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 Sie können die Deklaration eines Standardnamespace in der XML-Konstruktion rückgängig machen, nicht jedoch die Deklaration eines Namespacepräfixes. Die folgende Abfrage gibt einen Fehler zurück, da Sie die Deklaration des in der Konstruktion des <`b`>-Elements angegebenen Präfixes nicht rückgängig machen können.  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 Der neu konstruierte Namespace steht zum Verwenden innerhalb der Abfrage zur Verfügung. Die folgende Abfrage deklariert beispielsweise einen Namespace für die Konstruktion des <`FirstLocation`>-Elements und gibt das Präfix in den Ausdrücken für die LocationID- und SetupHrs-Attributwerte an.  
  
```  
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 Beachten Sie, dass das Erstellen eines neuen Namespacepräfixes in dieser Weise alle eventuell bereits vorhandenen Namespacedeklarationen für dieses Präfix überschreibt. Beispielsweise wird die Namespacedeklaration `AWMI="http://someURI"` im Prolog der Abfrage durch die Namespacedeklaration im <`FirstLocation`>-Element überschrieben.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://someURI";  
        <FirstLocation xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>Verwenden eines Prologs zum Hinzufügen von Namespaces  
 Dieses Beispiel veranschaulicht, wie dem konstruierten XML-Code Namespaces hinzugefügt werden können. Es wird ein Standardnamespace im Prolog der Abfrage hinzugefügt.  
  
```  
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 Beachten Sie, dass das Namespacedeklarationsattribut in der Konstruktion des <`b`>-Elements mit einer leeren Zeichenfolge als Wert angegeben ist. Dies macht die Deklaration des Standardnamespace des übergeordneten Elements rückgängig.  
  
```  
This is the result:  
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>XML-Konstruktion und Behandlung von Leerzeichen  
 Der Inhalt von Elementen in XML-Konstruktionen kann Leerzeichen enthalten. Diese Zeichen werden auf folgende Weise verarbeitet:  
  
-   Die Leerzeichen in Namespace-URIs werden als XSD-Typ behandelt **AnyURI**. Im Einzelnen werden sie behandelt wie folgt:  
  
    -   Leerzeichen am Anfang und am Ende werden entfernt.  
  
    -   Interne Leerzeichenwerte werden zu einem einzigen Leerzeichen zusammengefasst  
  
-   Zeilenvorschubzeichen innerhalb des Attributinhalts werden durch Leerzeichen ersetzt. Alle anderen Leerzeichen bleiben unverändert.  
  
-   Leerzeichen innerhalb von Elementen werden beibehalten.  
  
 Das folgende Beispiel veranschaulicht die Behandlung von Leerzeichen beim Konstruieren von XML-Code:  
  
```  
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   http://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 Dies ist das Ergebnis:  
  
```  
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>Andere direkte XML-Konstruktoren  
 Die Konstruktoren für Verarbeitungsanweisungen und XML-Kommentare verwenden dieselbe Syntax wie die ihnen entsprechenden XML-Konstrukte. Berechnete Konstruktoren für Textknoten werden ebenfalls unterstützt. Sie werden jedoch hauptsächlich zum Konstruieren von Textknoten in der XML-Datenbearbeitungssprache verwendet.  
  
 **Hinweis** ein Beispiel der Verwendung einer expliziten textknotenkonstruktors finden Sie unter Beispiel in [einfügen &#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md).  
  
 In der folgenden Abfrage enthält der konstruierte XML-Code ein Element, zwei Attribute, einen Kommentar und eine Verarbeitungsanweisung. Beachten Sie, dass vor <`FirstLocation`> ein Komma steht, da eine Sequenz konstruiert wird.  
  
```  
SELECT Instructions.query('  
  declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
/FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>Verwenden von berechneten Konstruktoren  
 aus. In diesem Fall geben Sie die Schlüsselwörter an, die den Typ des zu konstruierenden Knotens identifizieren. Es werden nur folgende Schlüsselwörter unterstützt:  
  
-   element  
  
-   Attribut  
  
-   text  
  
 Bei Element- und Attributknoten folgen auf diese Schlüsselwörter der Knotenname sowie der Ausdruck in geschweiften Klammern, der den Inhalt dieses Knotens generiert. Im folgenden Beispiel wird dieser XML-Code konstruiert:  
  
```  
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 Im Folgenden wird die Abfrage gezeigt, die die berechneten Konstruktoren zum Generieren des XML-Codes verwendet:  
  
```  
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 Der Ausdruck, der den Knoteninhalt generiert, kann einen Abfrageausdruck angeben.  
  
```  
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 Beachten Sie, dass die berechneten Element- und Attributkonstruktoren ermöglichen, Knotennamen zu berechnen, wie in der XQuery-Spezifikation definiert. Wenn Sie direkte Konstruktoren in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwenden, müssen Sie die Knotennamen, wie Element und Attribut, als konstante Literale angeben. Daher gibt es in Bezug auf Elemente und Attribute zwischen dem direkten und dem berechneten Konstruktor keinen Unterschied.  
  
 Im folgenden Beispiel wird der Inhalt für die konstruierten Knoten aus der XML-fertigungsanweisungen in der Instructions-Spalte der gespeicherten abgerufen der **Xml** -Datentyp in der ProductModel-Tabelle.  
  
```  
SELECT Instructions.query('  
  declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>Zusätzliche Implementierungseinschränkungen  
 Berechnete Attributkonstruktoren können nicht zum Deklarieren eines neuen Namespace verwendet werden. Außerdem werden in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die folgenden berechneten Konstruktoren nicht unterstützt:  
  
-   Berechnete Konstruktoren für Dokumentknoten  
  
-   Berechnete Konstruktoren für Verarbeitungsanweisungen  
  
-   Berechnete Konstruktoren für Kommentare  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Expressions (XQuery-Ausdrücke)](../xquery/xquery-expressions.md)  
  
  
