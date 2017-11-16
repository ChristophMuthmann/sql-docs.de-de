---
title: "Untergeordnete SELECT-Ausdrücke in Abfragen | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 918c7727a7af1f85f93d110652da450f1ea770cb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="subselects-in-queries"></a>Unterauswahlen in Abfragen
  Unterauswahlausdrücke werden SELECT-Ausdrücke geschachtelt, die verwendet werden, um das Leerzeichen des Cubes einzuschränken, von wo der äußere externe SELECT ausgewertet wird. Unterauswahlen ermöglichen es Ihnen, ein neues Leerzeichen zu definieren, über dem alle Berechnungen ausgewertet werden.  
  
## <a name="subselects-by-example"></a>Unterauswahlen zum Beispiel  
 Beginnen wir mit einem Beispiel, wie Unterauswahlen helfen können, die Ergebnisse zu erzeugen, die wir anzeigen möchten. Angenommen, Sie werden gebeten, eine Tabelle zu erzeugen, in der das Verkaufsverhalten für ein Jahr für die obersten 10 Produkte angezeigt wird.  
  
 Das Ergebnis sollte wie die folgende Tabelle aussehen:  
  
|||||  
|-|-|-|-|  
||Summe von Jahren|Jahr 1|...|  
|Summe der ersten 10 Produkte||||  
|Product A||||  
|...||||  
  
 Das o. a. Ergebnis könnte mit dem folgenden MDX-Ausdruck erreicht werden:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 Dies gibt die folgenden Ergebnisse zurück:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2005|CY 20062|CY 2007|KJ 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Straße 350 W Gelb, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 Dieses ist sehr in der Nähe an dem, nach dem wir suchen; außer dass die Abfrage 9 von 10 Produkten von den Allen Produkten-Gesamtbetrag zurückgegeben hat. Dies reflektiert der Summe aller Produkte und nicht die Summe von den zurückgegebenen Ersten 9 (in diesem Fall). Ein anderer Ansatz zur Lösung des Problems wird in der folgenden MDX-Abfrage dargestellt:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 Dies gibt die folgenden Ergebnisse zurück:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2005|KJ 2006|CY 2007|KJ 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Straße 350 W Gelb, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 Dies lag sehr nahe am gewünschten Ergebnisses, da nur die Summe der Produkte nicht korrekt ist. An diesem Punkt kann man anfangen, den oben erwähnten MDX-Ausdruck zu ändern, um die fehlende Zeile hinzuzufügen. Jedoch könnte sich diese Aufgabe als aufwändig erweisen.  
  
 Ein anderer Ansatz zur Lösung des Problems besteht in der Neudefinierung des Cuberaums, über den der MDX-Ausdruck aufgelöst wird. Was, wenn der 'neue' Cube nur Daten von den ersten 10-Produkten enthält? Dieser Cube hat dann alle Elemente an die ersten zehn Produkte angepasst, und nun eine einfache Abfrage unsere Anforderungen auflösen würde.  
  
 Der folgende MDX-Ausdruck verwendet eine Unterauswahlanweisung, um den Cuberaum für die ersten 10 Produkte neu zu definieren, um die gewünschten Ergebnisse zu erzeugen:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Der vorangehende Ausdruck gibt die folgenden Ergebnisse zurück:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2005|KJ 2006|CY 2007|KJ 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 Black, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Straße 350 W Gelb, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 Die o.a. Ergebnisse sind das, nach dem wir gesucht haben.  
  
 Überprüfen wir das was die Unterauswahl genau für uns gemacht hat. Die Unterauswahl hat für uns einen neuen Cube zurückgegeben, der alle anderen Dimensionen von Produkt wie sie sind, enthält; aber, in der Produktdimension hat es alle Elemente gefiltert, um eine Entsprechung für die obersten zehn Produkte zu finden, für die wir uns interessiert haben. Es war, als ob wir alle Daten entfernt haben, die die ersten 10 Kriterien nicht getroffen und den Cube neu erstellt haben. Das andere wichtige Konzept, um in diesem Beispiel zu verstehen, ist die Tatsache, dass die ersten 10 Produkte aller Elemente aller anderen Dimensionen im Cube hinüber berechnet wurden; das Frühere hat den Wert true, da keine anderen Filtereinschränkungen in der Unterauswahl auferlegt wurden.  
  
 Unterauswahlen können so komplex sein, wie gewünscht; im folgenden Beispiel wird veranschaulicht, wie eine ähnliche Tabelle wie die oben erwähnte erzeugt wird, die jedoch in der Sales Territory-Dimension nach France und in der Sales Channel-Dimension nach Internet gefiltert wird.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Ergibt die folgenden Ergebnisse:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|KJ 2005|KJ 2006|CY 2007|KJ 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 Black, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Straße 350 W Gelb, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 Die oben erwähnten Ergebnisse sind die in Frankreich durch den Internetchannel verkauften Erste 10-Produkte.  
  
## <a name="subselect-statement"></a>Unterauswahlanweisung  
 Das BNF für die Unterauswahl ist:  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 Die Unterauswahl ist eine andere Select-Anweisung wo die Achsenspezifikation und der SpezifikationsSlicer das Leerzeichen des Cubes, über denen das Äußere ausgewertet wird, auswählen.  
  
 Wenn ein Element in einer der Achse oder Slicerklausel angegeben wird, dann werden mit diesem Element seine Vorgänger und Nachfolger in den Untercuberaum für die Unterauswahl berücksichtigt; nicht alle gleichgeordneten Elemente in der Achse oder Slicerklausel werden erwähnt sowie deren Filterung der Nachfolger vom Teilbereich. Auf diese Weise wurde das Leerzeichen der äußeren Abfrage auf die vorhandenen Elemente in der Achsenklausel oder Slicerklausel, mit ihren Vorfahren und Nachfolgern wie oben erwähnt, beschränkt.  
  
 Da Alles Elemente zu allen nichterwähnten Dimensionen in Achse oder Slicerklauseln der auserlesenen Leerzeichen gehören; daher sind alle Nachfolger der Alles Elemente von diesen Dimensionen also ein Teil der Unterauswahlleerzeichen.  
  
 Das Alles Element wird, in allen Dimensionen, im Teilcubeleerzeichen, neu bewertet, um die Auswirkungen davon zu reflektieren das schränkt von neuen Leerzeichen ein.  
  
 Das folgende Beispiel zeigt, dass das, was oben gesagt wurde; der erste MDX-Ausdruck hilft, die ungefilterten Werte im Cube anzuzeigen, die zweite MDX veranschaulicht den Effekt der Filterung in der Subselect-Klausel:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 Gibt folgende Werte zurück:  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|United States|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 Im oben erwähnten Beispiel ist Seattle ein untergeordnetes Element von Washington, Portland ist ein untergeordnetes Element von Oregon, Oregon und Washington sind untergeordnete Elemente von USA, und USA ist ein untergeordnetes Element von [Customer Geography] [All Customers]. Alle angezeigten Elemente in diesem Beispiel verfügen über andere gleichgeordnete Elemente, die zum übergeordneten Aggregatwert beitragen; d. h. sind Spokane, Tacoma und Everett gleichgeordnete Orte von Seattle und ihnen, die alle nach Washington Internet Sales Amount beitragen. Wiederverkäuferumsatzwert ist von Kundengeografieattribut unabhängig; also wird der All-Wert in den Ergebnissen angezeigt. Der nächste MDX-Ausdruck veranschaulicht den Filtereffekt der Unterauswahlklausel:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 Gibt folgende Werte zurück:  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 Die Ergebnisse oben zeigen Sie an, dass nur Vorfahren und Nachfolger von Washington State Teil des Teilbereichs sind, wo die äußere Wählanweisung ausgewertet wurde; Oregon und Portland wurden aus dem Teilcube entfernt, da Oregon und alle anderen gleichgeordneten Status nicht in der Unterauswahl erwähnt wurden, als Washington erwähnt wurde.  
  
 Das Element Alles wurde angepasst, um die Filterung auf Washington zu reflektieren; wurde nicht nur in der Dimension [Kundengeografie] angepasst, sondern auch in allen anderen Dimensionen, die sich mit der Kundengeografie überschneiden. Alle Dimensionen, die sich nicht damit schneiden [z. B. Kundengeografie] bleiben im Teilcube unverändert.  
  
 Die folgenden zwei MDX-Anweisungen veranschaulichen wie das Element Alles in anderen Dimensionen verstellt wird, um den Filtereffekt der Unterauswahl zu treffen. Die erste Abfrage zeigt die unveränderten Ergebnisse an, und die Zweite zeigt folgende Auswirkungen der Filterung:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Zubehör|Components|Mountain|Straße|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|United States|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Zubehör|Components|Mountain|Straße|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|United States|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 Die oben erwähnten Ergebnisse zeigen an, dass - wie erwartet - die Werte aller Werte nur auf Washington Staat eingestellt wurden.  
  
 Unterauswahlen können ohne Grenze endlos tiefe Unterauswahlen schachteln, außer bei verfügbaren Speicher. Die innere meiste Unterauswahl definiert den Startteilbereich über dem die Filterung übernommen wird und auf das nächste Äußere übergeben wird. Eine wichtige Sache ist zu beachten; Schachtelung ist kein auswechselbarer Vorgang; deshalb erzeugt die Reihenfolge, in der die Schachtelung stattfindet, in Meinen Produkten unterschiedliche Ergebnisse. In den folgenden Beispielen sollte der Unterschied beim Auswählen einer Schachtelungsreihenfolge veranschaulicht werden.  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Folgende Ergebnisse wurden ausgegeben:  
  
||||||||  
|-|-|-|-|-|-|-|  
||Alle Vertriebsgebiete|Australia|Canada|Zentral|Nordwest|Südwest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Folgende Ergebnisse wurden ausgegeben:  
  
||||||||  
|-|-|-|-|-|-|-|  
||Alle Vertriebsgebiete|Australia|Canada|Nordwest|Südwest|United Kingdom|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 Wie Sie sehen können, gibt es zwischen beiden Sätzen Unterschiede in den Ergebnissen. Die erste Abfrage hat die Frage von den besten verkaufenden Produkte der obersten fünf verkaufenden Bereiche beantwortet. die zweite Abfrage hat die Frage der größten Verkäufe der obersten fünf verkaufenden Produkte beantwortet.  
  
### <a name="remarks"></a>Hinweise  
 Unterauswahlen haben folgende Einschränkungen und Beschränkungen:  
  
-   Die WHERE-Klausel filtert den Teilbereich nicht.  
  
-   Die WHERE-Klausel ändert nur das Standardelement in der Untercube.  
  
-   Die NON EMPTY-Klausel wird nicht in einer Achsenklausel zugelassen; verwenden Sie stattdessen einen [NonEmpty &#40;MDX&#41;](../../../mdx/nonempty-mdx.md)-Funktionsausdruck.  
  
-   Die HAVING-Klausel wird nicht in einer Achsenklausel zugelassen; verwenden Sie stattdessen einen [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)-Funktionsausdruck.  
  
-   Standardmäßig sind berechnete Elemente in untergeordneten SELECT-Ausdrücken nicht zulässig; allerdings diese Einschränkung kann geändert werden, in einer sitzungsbasis durch Zuweisen eines Werts, der **Unterabfragen** Verbindungszeichenfolgeneigenschaft in <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> oder **DBPROP_MSMD_SUBQUERIES** Eigenschaft im [ Unterstützte XMLA-Eigenschaften &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md). Eine genaue Erklärung des Verhaltens berechneter Elemente, abhängig von den Werten von [SubQueries](../../../analysis-services/multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) oder **DBPROP_MSMD_SUBQUERIES** , finden Sie unter **Berechnete Elemente in untergeordneten SELECT-Ausdrücken und Teilcubes**.  
  
  

