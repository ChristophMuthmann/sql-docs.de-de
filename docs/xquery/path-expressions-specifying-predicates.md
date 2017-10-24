---
title: "Angeben von Prädikaten in einem Pfadausdrucksschritt | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
- axis step [XQuery]
- predicates [XQuery]
- qualifiers [XQuery]
- path expressions [XQuery]
ms.assetid: 2660ceca-b8b4-4a1f-98a0-719ad5f89f81
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5b417b2bfe5d995657ad86cf44b650b751f6a30
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="path-expressions---specifying-predicates"></a>Path-Ausdrücken - angeben von Prädikaten
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Im Thema beschriebene [Pfadausdrücke in XQuery](../xquery/path-expressions-xquery.md), ein achsenschritt in einem Pfadausdruck umfasst die folgenden Komponenten:  
  
-   [Eine Achse](../xquery/path-expressions-specifying-axis.md).  
  
-   Einen Knotentest. Weitere Informationen finden Sie unter [Knotentest angeben, in einem Pfadausdrucksschritt](../xquery/path-expressions-specifying-node-test.md).  
  
-   Null oder mehr Prädikate. Diese Eingabe ist optional.  
  
 Das optionale Prädikat ist der dritte Teil des Achsenschritts in einem Pfadausdruck.  
  
## <a name="predicates"></a>Prädikate  
 Ein Prädikat wird zum Filtern einer Knotensequenz durch Anwenden eines angegebenen Tests verwendet. Der Prädikatausdruck ist in eckige Klammern eingeschlossen und an den letzten Knoten in einem Pfadausdruck gebunden.  
  
 Nehmen wir beispielsweise an, die ein SQL-Parameterwert (X) von der **Xml** -Datentyp deklariert wird, wie im folgenden gezeigt:  
  
```  
declare @x xml  
set @x = '  
<People>  
  <Person>  
    <Name>John</Name>  
    <Age>24</Age>  
  </Person>  
  <Person>  
    <Name>Goofy</Name>  
    <Age>54</Age>  
  </Person>  
  <Person>  
    <Name>Daffy</Name>  
    <Age>30</Age>  
  </Person>  
</People>  
'  
```  
  
 In diesem Fall sind die folgenden Ausdrücke gültig, die einen Prädikatwert von [1] für jede der drei unterschiedlichen Knotenebenen verwenden:  
  
```  
select @x.query('/People/Person/Name[1]')  
select @x.query('/People/Person[1]/Name')  
select @x.query('/People[1]/Person/Name')  
```  
  
 Beachten Sie, dass in jedem Fall das Prädikat an den Knoten im Pfadausdruck gebunden wird, für den es angewendet wird. Beispielsweise wählt der erste Pfadausdruck jeweils das erste <`Name`>-Element im entsprechenden /People/Person-Knoten aus und gibt mit der bereitgestellten XML-Instanz Folgendes zurück:  
  
```  
<Name>John</Name><Name>Goofy</Name><Name>Daffy</Name>  
```  
  
 Der zweite Pfadausdruck wählt alle <`Name`>-Elemente unter dem /People/Person-Knoten aus. Deshalb gibt er das folgende Ergebnis zurück:  
  
```  
<Name>John</Name>  
```  
  
 Es können auch Klammern verwendet werden, um die Auswertungsreihenfolge des Prädikats zu ändern. So wird z. B. im folgenden Ausdruck ein Klammernsatz verwendet, um den Pfad von (/People/Person/Name) vom Prädikat [1] zu trennen:  
  
```  
select @x.query('(/People/Person/Name)[1]')  
```  
  
 In diesem Beispiel ändert sich die Reihenfolge, in der das Prädikat angewendet wird. Das liegt daran, dass der in Klammern eingeschlossene Pfad (/People/Person/Name) zuerst ausgewertet und anschließend der Prädikatoperator [1] für das Set angewendet wird, das alle mit dem eingeschlossenen Pfad übereinstimmenden Knoten enthält. Ohne die Klammern wäre die Reihenfolge des Vorgangs anders: Der Prädikatoperator [1] würde dann als ein `child::Name`-Knotentest angewendet werden, wie das im ersten Beispiel für den Pfadausdruck der Fall war.  
  
### <a name="quantifiers-and-predicates"></a>Quantifizierer und Prädikate  
 Quantifizierer können innerhalb der Klammern des Prädikats mehrfach verwendet und hinzugefügt werden. So wäre z. B. unter Nutzung des vorigen Beispiels folgende Verwendung von mehreren Quantifizierern innerhalb eines komplexen Prädikatunterausdrucks gültig.  
  
```  
select @x.query('/People/Person[contains(Name[1], "J") and xs:integer(Age[1]) < 40]/Name/text()')  
```  
  
 Das Ergebnis eines Prädikatausdrucks wird in einen booleschen Wert konvertiert und wird als Wahrheitswert des Prädikats bezeichnet. Im Ergebnis werden nur die Knoten in der Sequenz zurückgegeben, deren Prädikatwahrheitswert True ist. Alle anderen Knoten werden verworfen.  
  
 Beim folgenden Pfadausdruck ist z. B. ein Prädikat in den zweiten Schritt eingeschlossen:  
  
```  
/child::root/child::Location[attribute::LocationID=10]  
```  
  
 Die von diesem Prädikat angegebene Bedingung wird auf alle untergeordneten Elemente des <`Location`>-Knotens angewendet. Das führt dazu, dass als Ergebnis nur solche Arbeitsplatzstandorte zurückgegeben werden, bei denen der Attributwert der Standortkennung (LocationID) 10 ist.  
  
 Der vorige Pfadausdruck wird in der folgenden SELECT-Anweisung ausgeführt:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
 /child::AWMI:root/child::AWMI:Location[attribute::LocationID=10]  
')  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
### <a name="computing-predicate-truth-values"></a>Berechnen des Prädikatwahrheitswerts  
 Gemäß den XQuery-Spezifikationen werden die folgenden Regeln angewendet, um den Prädikatwahrheitswert zu ermitteln:  
  
1.  Wenn der Wert des Prädikatausdrucks eine leere Sequenz ist, ist der Prädikatwahrheitswert False.  
  
     Beispiel:  
  
    ```  
    SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     /child::AWMI:root/child::AWMI:Location[attribute::LotSize]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=7  
    ```  
  
     Der Pfadausdruck in dieser Abfrage gibt nur die <`Location`>-Elementknoten zurück, die über ein LotSize-Attribut verfügen. Wenn das Prädikat für einen bestimmten <`Location`> eine leere Sequenz zurückgibt, wird dieser Arbeitsplatzstandort nicht im Ergebnis zurückgegeben.  
  
2.  Werte können nur xs: Integer, xs: Boolean oder ein Knoten sein Prädikat\*. Für Knoten\*, das Prädikat zu "true", wenn alle Knoten vorhanden sind, und bei einer leeren Sequenz "false" ausgewertet wird. Alle anderen numerischen Typen wie z. B. double und float generieren einen statischen Typisierungsfehler. Der Prädikatwahrheitswert eines Ausdrucks ist ausschließlich dann True, wenn die resultierende ganze Zahl gleich dem Wert der Kontextposition ist. Darüber hinaus nur Integer-Literalwerte und die **last()** -Funktion verringern die Kardinalität des gefilterten schrittausdrucks auf 1.  
  
     Beispielsweise ruft die folgende Abfrage den dritten untergeordneten Elementknoten des <`Features`>-Elements ab.  
  
    ```  
    SELECT CatalogDescription.query('  
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /child::PD:ProductDescription/child::PD:Features/child::*[3]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=19  
    ```  
  
     Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
    -   Der dritte Schritt im Ausdruck gibt einen Prädikatausdruck mit dem Wert 3 an. Daher ist der Prädikatwahrheitswert dieses Ausdrucks nur für die Knoten True, deren Kontextposition 3 ist.  
  
    -   Der dritte Schritt gibt auch ein Platzhalterzeichen (*) an, das alle Knoten im Knotentest anzeigt. Das Prädikat filtert jedoch die Knoten und gibt nur den Knoten in der dritten Position zurück.  
  
    -   Die Abfrage gibt den dritten untergeordneten Knoten der untergeordneten <`Features`>-Elemente für die untergeordneten <`ProductDescription`>-Elemente des Dokumentenstamms zurück.  
  
3.  Wenn der Wert des Prädikatausdrucks ein einfacher Werttyp des booleschen Datentyps ist, entspricht der Prädikatwahrheitswert dem Wert des Prädikatausdrucks.  
  
     Die folgende Abfrage wird z. B. angegeben, für eine **Xml**Variablen vom Typ, der eine XML-Instanz, die Kunden Umfrage XML-Instanz enthält. Die Abfrage ruft solche Kunden ab, die über untergeordnete Elemente verfügen. In dieser Abfrage wird das wäre \<HasChildren > 1\</HasChildren >.  
  
    ```  
    declare @x xml  
    set @x='  
    <Survey>  
      <Customer CustomerID="1" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>1</HasChildren>  
      </Customer>  
      <Customer CustomerID="2" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>0</HasChildren>  
      </Customer>  
    </Survey>  
    '  
    declare @y xml  
    set @y = @x.query('  
      for $c in /child::Survey/child::Customer[( child::HasChildren[1] cast as xs:boolean ? )]  
      return   
          <CustomerWithChildren>  
              { $c/attribute::CustomerID }  
          </CustomerWithChildren>  
    ')  
    select @y  
    ```  
  
     Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
    -   Der Ausdruck in der **für** -Schleife umfasst zwei Schritte, und der zweite Schritt gibt ein Prädikat. Der Wert dieses Prädikats ist ein Wert des booleschen Datentyps. Wenn dieser Wert True ist, so ist auch der Wahrheitswert des Prädikats True.  
  
    -   Die Abfrage gibt die <`Customer`> Element untergeordnete Elemente, mit dem Prädikatwert ist "true", der die \<Umfrage > Element untergeordnete Elemente des Basisverzeichnisses. Dies ist das Ergebnis:  
  
        ```  
        <CustomerWithChildren CustomerID="1"/>   
        ```  
  
4.  Wenn der Wert des Prädikatausdrucks eine Sequenz ist, die mindestens einen Knoten enthält, so ist der Wahrheitswert des Prädikats True.  
  
 Die folgende Abfrage ruft z. B. ProductModelID für Produktmodelle, deren XML-katalogbeschreibung mindestens eine Funktion, die ein untergeordnetes Element von enthält, der <`Features`>-Element aus dem Namespace zugeordnet der **Wm**Präfix.  
  
```  
SELECT ProductModelID  
FROM   Production.ProductModel  
WHERE CatalogDescription.exist('  
             declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
             /child::PD:ProductDescription/child::PD:Features[wm:*]  
             ') = 1  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die WHERE-Klausel gibt die [EXIST()-Methode (XML-Datentyp)](../t-sql/xml/exist-method-xml-data-type.md).  
  
-   Der Path-Ausdruck innerhalb der **exist()** Methode gibt ein Prädikat im zweiten Schritt. Wenn der Prädikatausdruck eine Sequenz von mindestens einer Funktion zurückgibt, ist der Wahrheitswert dieses Prädikatausdrucks True. In diesem Fall, da die **exist()** -Methode True zurückgibt, wird die Produktmodell-ID zurückgegeben.  
  
## <a name="static-typing-and-predicate-filters"></a>Statische Typisierung und Prädikatfilter  
 Die Prädikate können sich auch auf den statisch abgeleiteten Typ eines Ausdrucks auswirken. Integer-Literalwerte und die **last()** -Funktion verringern die Kardinalität des gefilterten schrittausdrucks zumeist auf 1.  
  
  

