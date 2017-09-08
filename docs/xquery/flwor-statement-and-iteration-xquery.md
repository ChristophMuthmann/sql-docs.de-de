---
title: FLWOR-Anweisung und-Iteration (XQuery) | Microsoft Docs
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
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0aecf7bfdb57a53c0c0cbbd8f4c2ccbaf9a9862d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR-Anweisung und -Iteration (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery definiert die Iterationssyntax FLWOR. FLWOR ist das Akronym für `for`, `let`, `where`, `order by` und `return`.  
  
 Eine FLWOR-Anweisung besteht aus den folgenden Teilen:  
  
-   Einer oder mehreren FOR-Klauseln, die eine oder mehrere Iteratorvariablen an Eingabesequenzen binden.  
  
     Eingabesequenzen können andere XQuery-Ausdrücke wie z. B. XPath-Ausdrücke sein. Es handelt sich entweder um Sequenzen von Knoten oder um Sequenzen atomarer Werte. Sequenzen atomarer Werte können mithilfe von Literalen oder Konstruktorfunktionen erstellt werden. Erstellte XML-Knoten sind als Eingabesequenzen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nicht zulässig.  
  
-   Einer optionalen `let`-Klausel. Diese Klausel weist der angegebenen Variable für eine bestimmte Iteration einen Wert zu. Der zugewiesene Ausdruck kann ein XQuery-Ausdruck, z. B. ein XPath-Ausdruck sein, und entweder eine Sequenz aus Knoten oder eine Sequenz aus atomaren Werten zurückgeben. Sequenzen aus atomaren Werten können mithilfe von Literalen oder Konstruktorfunktionen erstellt werden. Erstellte XML-Knoten sind als Eingabesequenzen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nicht zulässig.  
  
-   Einer Iteratorvariablen. Diese Variable kann eine optionale Typassertion mithilfe des `as`-Schlüsselworts besitzen.  
  
-   Einer optionalen `where`-Klausel. Diese Klausel wendet ein Filterprädikat auf die Iteration an.  
  
-   Einer optionalen `order by`-Klausel.  
  
-   Einem `return`-Ausdruck. Der Ausdruck in der `return`-Klausel erstellt das Ergebnis der FLWOR-Anweisung.  
  
 Die folgende Abfrage führt z. B. eine Iteration durch die <`Step`>-Elemente am ersten Produktionsstandort durch und gibt den Zeichenfolgenwert der <`Step`>-Knoten zurück:  
  
```  
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 Dies ist das Ergebnis:  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 Die folgende Abfrage ähnelt der vorherigen Abfrage, wird jedoch für die Instructions-Spalte, eine typisierte xml-Spalte, der ProductModel-Tabelle angegeben. Die Abfrage führt eine Iteration durch alle Fertigungsschritte (die <`step`>-Elemente) am ersten Arbeitsplatzstandort für ein bestimmtes Produkt aus.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   `$Step` ist die Iteratorvariable.  
  
-   Die [Pfadausdruck](../xquery/path-expressions-xquery.md), `//AWMI:root/AWMI:Location[1]/AWMI:step`, generiert die Eingabesequenz. Diese Sequenz ist die Sequenz der untergeordneten <`step`>-Elementknoten des ersten <`Location`>-Elementknotens.  
  
-   Die optionale Prädikatklausel `where` wird nicht verwendet.  
  
-   Der `return`-Ausdruck gibt einen Zeichenfolgenwert aus dem <`step`>-Element zurück.  
  
 Die [string-Funktion (XQuery)](../xquery/data-accessor-functions-string-xquery.md) dient zum Abrufen von der String-Wert, der die <`step`> Knoten.  
  
 Dies ist das Teilergebnis:  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 Die folgenden Beispiele zeigen weitere zusätzliche Eingabesequenzen, die zulässig sind:  
  
```  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sind heterogene Sequenzen nicht zulässig. Insbesondere sind Sequenzen, die eine Mischung aus atomaren Werten und Knoten enthalten, nicht zulässig.  
  
 Iteration wird häufig verwendet, zusammen mit den [XML-Konstruktion](../xquery/xml-construction-xquery.md) -Syntax zum Transformieren von XML-Formate, wie in der nächsten Abfrage gezeigt.  
  
 In der AdventureWorks-Beispieldatenbank, die produktionsanweisungen gespeichert, der **Anweisungen** Spalte die **Production.ProductModel** Tabelle folgende Form aufweisen:  
  
```  
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 Die folgende Abfrage erstellt neues XML, in dem die <`Location`>-Elemente mit den Arbeitsplatzstandort-Attributen als untergeordnete Elemente zurückgegeben werden:  
  
```  
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SteupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 Im Folgenden wird die Abfrage aufgeführt:  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die FLWOR-Anweisung ruft eine Sequenz von <`Location`>-Elementen für ein bestimmtes Produkt ab.  
  
-   Die [Data-Funktion (XQuery)](../xquery/data-accessor-functions-data-xquery.md) wird verwendet, um den Wert der einzelnen Attribute zu extrahieren, damit sie auf das sich ergebende XML als Textknoten statt als Attribute hinzugefügt werden.  
  
-   Der Ausdruck in der RETURN-Klausel erstellt das von Ihnen gewünschte XML.  
  
 Dies ist ein Teilergebnis:  
  
```  
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>Verwenden der let-Klausel  
 Mithilfe der `let`-Klausel können Sie wiederholte Ausdrücke benennen, auf die Sie durch einen Verweis auf die Variable verweisen können. Der Ausdruck, der einer `let`-Variable zugewiesen ist, wird jedes Mal in die Abfrage eingefügt wird, wenn in der Abfrage auf die Variable verwiesen wird. Das bedeutet, dass die Anweisung so oft ausgeführt wird, wie auf den Ausdruck verwiesen wird.  
  
 In der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]-Datenbank enthalten die Produktionsanweisungen Informationen zu den erforderlichen Tools und der Position, an der die Tools verwendet werden. In der folgenden Abfrage wird die `let`-Klausel verwendet, um die Tools, die zum Erstellen eines Produktionsmodells erforderlich sind, sowie die Positionen aufzulisten, an denen die einzelnen Tools benötigt werden.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>Verwenden der where-Klausel  
 Mit der `where`-Klausel können Sie die Ergebnisse einer Iteration filtern. Dies wird im folgenden Beispiel veranschaulicht.  
  
 Bei der Produktion eines Fahrrades durchläuft der Produktionsprozess eine Reihe von Arbeitsplatzstandorten. Jeder Arbeitsplatzstandort definiert eine Sequenz von Produktionsschritten. Die folgende Abfrage ruft nur die Arbeitsplatzstandorte ab, die ein Fahrradmodell fertigen und weniger als drei Produktionsschritte verwenden. Dies bedeutet, dass sie weniger als drei <`step`>-Elemente besitzen.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Beachten Sie in der vorhergehenden Abfrage Folgendes:  
  
-   Die `where` -Schlüsselwort verwendet, die **count()** Funktion, um die Anzahl der <`step`> untergeordnete-Elemente in jedem arbeitsplatzstandort.  
  
-   Der `return`-Ausdruck erstellt das von Ihnen gewünschte XML aus den Ergebnissen der Iteration.  
  
 Dies ist das Ergebnis:  
  
```  
<Location LocationID="30"/>   
```  
  
 Das Ergebnis des Ausdrucks in der `where`-Klausel wird mithilfe der folgenden Regeln in der angegebenen Reihenfolge in einen booleschen Wert konvertiert. Diese Regeln entsprechen den Regeln für Prädikate in path-Ausdrücken, nur sind keine ganzen Zahlen zulässig:  
  
1.  Wenn der `where`-Ausdruck eine leere Sequenz zurückgibt, ist der effektive boolesche Wert False.  
  
2.  Wenn der `where`-Ausdruck einen booleschen Wert vom simple-Typ zurückgibt, ist dieser Wert der effektive boolesche Wert.  
  
3.  Wenn der `where`-Ausdruck eine Sequenz zurückgibt, die mindestens einen Knoten enthält, ist der effektive boolesche Wert True.  
  
4.  Anderenfalls wird ein statischer Fehler ausgelöst.  
  
## <a name="multiple-variable-binding-in-flwor"></a>Binden mehrerer Variablen in FLWOR  
 Sie können einen einzelnen FLWOR-Ausdruck verwenden, um mehrere Variablen an Eingabesequenzen zu binden. Im folgenden Beispiel wird die Abfrage z. B. für eine nicht typisierte xml-Variable angegeben. Der FLOWR-Ausdruck gibt das erste untergeordnete <`Step`>-Element in jedem <`Location`>-Element zurück.  
  
```  
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die `for` Ausdruck definiert `$Loc` und $`FirstStep` Variablen.  
  
-   Die `two`-Ausdrücke `/ManuInstructions/Location` und `$FirstStep in $Loc/Step[1]` sind insofern korreliert, als die Werte von `$FirstStep` von den Werten von `$Loc` abhängen.  
  
-   Der `$Loc` zugeordnete Ausdruck generiert eine Sequenz von <`Location`>-Elementen. Für jedes <`Location`>-Element generiert `$FirstStep` eine Sequenz aus einem <`Step`>-Element, ein Singleton.  
  
-   `$Loc` wird in dem Ausdruck angegeben, der der `$FirstStep`-Variablen zugeordnet ist.  
  
 Dies ist das Ergebnis:  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 Die folgende Abfrage ist ähnlich, außer dass sie für die Instructions-Spalte, die typisierte angegeben ist **Xml** Spalte, der die **ProductModel** Tabelle. [XML-Konstruktion (XQuery)](../xquery/xml-construction-xquery.md) wird verwendet, um den XML-Code generieren möchten.  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Beachten Sie in der vorhergehenden Abfrage Folgendes:  
  
-   Die `for`-Klausel definiert zwei Variablen, `$WC` und `$S`. Der Ausdruck, der `$WC` zugeordnet ist, generiert eine Sequenz von Arbeitsplatzstandorten bei der Fertigung eines Fahrrades eines Fahrradproduktmodells. Der path-Ausdruck, der der `$S`-Variablen zugeordnet ist, generiert eine Sequenz von Schritten für jede Arbeitsplatzstandort-Sequenz in `$WC`.  
  
-   Die rückgabeanweisung erstellt XML, in dem ein <`Step`>-Element, das den Produktionsschritt enthält und die **LocationID** als Attribut.  
  
-   Die **deklarieren standardelementnamespace** im XQuery-Prolog verwendet wird, sodass alle Namespacedeklarationen im sich ergebenden XML am Element obersten Ebene angezeigt werden. Auf diese Weise ist das Ergebnis besser lesbar. Weitere Informationen zu Standardnamespaces finden Sie unter [Behandlung von Namespaces in XQuery](../xquery/handling-namespaces-in-xquery.md).  
  
 Dies ist das Teilergebnis:  
  
```  
<Step xmlns=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>Verwenden der order by-Klausel  
 Die Sortierung in XQuery wird mithilfe der `order by`-Klausel im FLWOR-Ausdruck ausgeführt. Übergebenen Sortierausdrücke, um die `order by` Klausel muss Rückgabewerte, deren Typen für gelten, die **Gt** Operator. Jeder Sortierausdruck muss zu einer Singletonsequenz mit einem Element führen. Standardmäßig wird die Sortierung in aufsteigender Reihenfolge durchgeführt. Sie können optional die auf- oder absteigende Reihenfolge für jeden Sortierausdruck angeben.  
  
> [!NOTE]  
>  Sortiervergleiche für Zeichenfolgenwerte, die von der XQuery-Implementierung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt werden, werden immer mithilfe der binären Unicode-Codepunktsortierung ausgeführt.  
  
 Die folgende Abfrage ruft alle Rufnummern für einen bestimmten Kunden aus der AdditionalContactInfo-Spalte ab. Die Ergebnisse werden nach Rufnummer sortiert.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 Beachten Sie, dass die [Atomisierung (XQuery)](../xquery/atomization-xquery.md) Prozess Ruft den atomaren Wert des der <`number`> Elemente vor der Übergabe an `order by`. Sie können den Ausdruck schreiben, mit der **data()** -Funktion, dies ist jedoch nicht erforderlich.  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 Dies ist das Ergebnis:  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 Statt die Namespaces im Abfrageprolog zu deklarieren, können Sie diese auch mithilfe von WITH XMLNAMESPACES deklarieren.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 Sie können auch nach Attributwert sortieren. Die folgende Abfrage ruft z. B. die neu erstellten <`Location`>-Elemente ab, deren LocationID- und LaborHours-Attribute nach dem LaborHours-Attribut in absteigender Reihenfolge sortiert sind. Als Ergebnis dieses Vorgangs werden die Arbeitsplatzstandorte, die die größte Anzahl von Arbeitsstunden aufweisen, zuerst zurückgegeben.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 In der folgenden Abfrage werden die Ergebnisse nach dem Elementnamen sortiert. Die Abfrage ruft die Spezifikationen eines bestimmten Produkts aus dem Produktkatalog ab. Die Spezifikationen sind die untergeordneten Elemente des <`Specifications`>-Elements.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace  
 pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Der `/p1:ProductDescription/p1:Specifications/*`-Ausdruck gibt untergeordnete Elemente von <`Specifications`> zurück.  
  
-   Der `order by (local-name($a))`-Ausdruck sortiert die Sequenz nach dem lokalen Namensanteil des Elementnamens.  
  
 Dies ist das Ergebnis:  
  
```  
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 Knoten, in denen der Sortierausdruck leer zurückgegeben wird, werden an den Beginn der Sequenz sortiert, wie das folgende Beispiel zeigt:  
  
```  
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 Sie können mehrere Sortierkriterien angeben, wie im folgenden Beispiel gezeigt wird. Die Abfrage in diesem Beispiel sortiert <`Employee`>-Elemente zuerst nach den Title- und dann nach den Administrator-Attributwerten.  
  
```  
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die Sortierausdrücke müssen homogen typisiert sein. Dies wird statisch überprüft.  
  
-   Das Sortieren leerer Sequenzen kann nicht gesteuert werden.  
  
-   Die empty least-, empty greatest- und collation-Schlüsselwörter für `order by` werden nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Expressions (XQuery-Ausdrücke)](../xquery/xquery-expressions.md)  
  
  
