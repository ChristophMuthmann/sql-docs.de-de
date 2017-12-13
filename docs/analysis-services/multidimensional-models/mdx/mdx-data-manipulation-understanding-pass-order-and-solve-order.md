---
title: "Grundlegendes zu Durchlauf- und Lösungsreihenfolge (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- evaluation order [MDX]
- calculation order [MDX]
- SOLVE_ORDER property
- queries [MDX], solve orders
- solve orders [MDX]
- pass orders [MDX]
- expressions [MDX], solve orders
ms.assetid: 7ed7d4ee-4644-4c5d-99a4-c4b429d0203c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9c3b028eb658f2f75d6e70ec9057f3f156ca5f05
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-data-manipulation---understanding-pass-order-and-solve-order"></a>MDX - Datenmanipulation: Grundlegendes zur Übergabe bestellen und Lösungsreihenfolge
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Wenn ein Cube als Ergebnis eines MDX-Skripts berechnet wird, können sie viele berechnungsphasen je nach der Verwendung verschiedener Berechnungsfunktionen Features durchlaufen. Jede Phase bezeichnet man als Berechnungsdurchlauf.  
  
 Auf einen Berechnungsdurchlauf kann durch eine Ordnungsposition verwiesen werden, die Berechnungsdurchlaufnummer genannt wird. Die Anzahl an Berechnungsdurchläufen, die für eine vollständige Berechnung aller Zellen eines Cubes erforderlich sind, wird als Berechnungsdurchlauftiefe des Cubes bezeichnet.  
  
 Faktentabelle und Rückschreibedaten wirken sich nur auf Durchlauf 0 aus. Skripts füllen Daten nach Durchlauf 0 auf. Durch jede Zuweisung und Berechnungsanweisung in einem Skript wird ein neuer Durchlauf erstellt. Außerhalb des MDX-Skripts beziehen sich Verweise auf den absoluten Durchlauf 0 auf den letzten Durchlauf, der durch das Skript für den Cube erstellt wurde.  
  
 Berechnete Elemente werden in allen Durchläufen erstellt, aber der Ausdruck wird auf den aktuellen Durchlauf angewendet. Vorherige Durchläufe enthalten das berechnete Measure, allerdings mit einem NULL-Wert.  
  
## <a name="solve-order"></a>Lösungsreihenfolge  
 Die Lösungsreihenfolge bestimmt die Priorität der Berechnung bei konkurrierenden Ausdrücken. Innerhalb eines einzelnen Durchlaufes bestimmt die Lösungsreihenfolge zwei Dinge:  
  
-   Die Reihenfolge, in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Dimensionen, Elemente, berechnete Elemente, benutzerdefinierte Rollups und berechnete Zellen auswertet.  
  
-   Die Reihenfolge, in der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] benutzerdefinierte Elemente, berechnete Elemente, benutzerdefinierte Rollups und berechnete Zellen berechnet.  
  
 Das Element mit der höchsten Lösungsreihenfolge hat Vorrang.  
  
> [!NOTE]  
>  Dies gilt jedoch nicht für die Aggregatfunktion. Mit der Aggregatfunktion berechnete Elemente haben eine niedrigere Lösungsreihenfolge als alle berechneten Measures, die eine Schnittmenge bilden.  
  
## <a name="solve-order-values-and-precedence"></a>Werte der Lösungsreihenfolge und Rangfolge  
 Werte der Lösungsreihenfolge können im Bereich von -8.181 bis 65.535 liegen. In diesem Bereich entsprechen einige Werte der Lösungsreihenfolge bestimmten Berechnungsarten, wie in der folgenden Tabelle gezeigt.  
  
|Berechnung|Lösungsreihenfolge|  
|-----------------|-----------------|  
|Benutzerdefinierte Elementformeln|-5119|  
|Unäre Operatoren|-5119|  
|Berechnung sichtbarer Gesamtwerte|-4096|  
|Alle anderen Berechnungen (wenn nicht anders angegeben)|0|  
  
 Beim Festlegen von Werten der Lösungsreihenfolge sollten Sie unbedingt nur positive ganze Zahlen verwenden. Wenn Sie Werte zuweisen, die niedriger sind als die in der vorherigen Tabelle angezeigten Werte der Lösungsreihenfolge, kann der Berechnungsdurchlauf unvorhersehbar werden. Angenommen, die Berechnung für ein berechnetes Element erhält einen Wert der Lösungsreihenfolge, der niedriger ist als der Standardformelwert für benutzerdefinierte Rollups von -5.119. Ein so niedriger Wert der Lösungsreihenfolge führt dazu, dass die berechneten Elemente vor den benutzerdefinierten Rollupformeln berechnet werden. Dies kann zu falschen Ergebnissen führen.  
  
### <a name="creating-and-changing-solve-order"></a>Erstellen und Ändern der Lösungsreihenfolge  
 Im Cube-Designer können Sie im Bereich **Berechnungen**die Lösungsreihenfolge für berechnete Elemente und berechnete Zellen ändern, indem Sie die Reihenfolge der Berechnungen ändern.  
  
 In MDX können Sie mit dem **SOLVE_ORDER** -Schlüsselwort berechnete Elemente und berechnete Zellen erstellen bzw. ändern.  
  
## <a name="solve-order-examples"></a>Beispiele für die Lösungsreihenfolge  
 Um die mögliche Komplexität der Lösungsreihenfolge zu veranschaulichen, beginnt die folgende Reihe von MDX-Abfragen mit zwei Abfragen, die einzeln betrachtet keine Probleme mit der Lösungsreihenfolge aufweisen. Die beiden Abfragen werden dann in einer Abfrage kombiniert, für die eine Lösungsreihenfolge erforderlich ist.  
  
> [!NOTE]  
>  Sie können diese MDX-Abfragen unter Verwendung der mehrdimensionalen Adventure Works-Beispieldatenbank ausführen. Sie können das Beispiel zu [AdventureWorks Multidimensional Models SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) von der Codeplex-Website herunterladen.  
  
### <a name="query-1differences-in-income-and-expenses"></a>Abfrage 1 – Differenzen zwischen Income und Expenses  
 Mit der ersten MDX-Abfrage berechnen Sie die Differenz zwischen Umsätzen und Kosten für jedes Jahr, indem Sie eine einfache MDX-Abfrage wie im folgenden Beispiel erstellen:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Diese Abfrage enthält als einziges berechnetes Element `Year Difference`. Da nur ein berechnetes Element vorhanden ist, stellt die Lösungsreihenfolge kein Problem dar, vorausgesetzt der Cube verwendet keine berechneten Elemente.  
  
 Mit dieser MDX-Abfrage wird ein der folgenden Tabelle ähnelndes Resultset erstellt.  
  
||Internet Sales Amount|Internet Total Product Cost|  
|-|---------------------------|---------------------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|  
|**KJ 2008**|$9,770,899.74|$5,721,205.24|  
|**Year Difference**|($20,160.56)|$2,878.06|  
  
### <a name="query-2percentage-of-income-after-expenses"></a>Abfrage 2 – Prozentsatz von Income nach Abzug von Expenses  
 Mit der zweiten Abfrage berechnen Sie den Prozentsatz des Einkommens nach Abzug der Ausgaben für jedes Jahr. Verwenden Sie dazu die folgende MDX-Abfrage:  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Wie die vorherige MDX-Abfrage enthält auch diese nur ein berechnetes Element, `Profit Margin`, und muss daher keine Lösungsreihenfolge berücksichtigen.  
  
 Mit dieser MDX-Abfrage wird ein etwas anderes Resultset erstellt, ähnlich der folgenden Tabelle.  
  
||Internet Sales Amount|Internet Total Product Cost|Profit Margin|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**KJ 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
  
 Der Grund für die unterschiedlichen Resultsets aus der ersten und der zweiten Abfrage ist eine andere Platzierung des berechneten Elements. In der ersten Abfrage ist das berechnete Element Teil der ROWS-Achse und nicht der COLUMNS-Achse, wie in der zweiten Abfrage. Diese unterschiedliche Platzierung gewinnt in der nächsten Abfrage an Bedeutung, wenn die beiden berechneten Elemente in einer einzigen MDX-Abfrage kombiniert werden.  
  
### <a name="query-3combined-year-difference-and-net-income-calculations"></a>Abfrage 3 – Kombinierte Berechnungen für Year Difference und Net Income  
 In dieser letzten Abfrage, in der die beiden vorherigen Beispiele in einer MDX-Abfrage kombiniert werden, ist die Lösungsreihenfolge von Bedeutung, da Berechnungen sowohl für Spalten als auch für Zeilen ausgeführt werden. Um sicherzustellen, dass die Berechnungen in der richtigen Reihenfolge vorgenommen werden, definieren Sie diese Reihenfolge mithilfe des **SOLVE_ORDER** -Schlüsselworts.  
  
 Das **SOLVE_ORDER** -Schlüsselwort gibt die Lösungsreihenfolge der berechneten Elemente in einer MDX-Abfrage oder einem **CREATE MEMBER** -Befehl an. Die mit dem **SOLVE_ORDER** -Schlüsselwort verwendeten ganzzahligen Werte sind relativ, müssen nicht mit 0 beginnen und nicht aufeinander folgen. Der Wert weist MDX lediglich an, ein Element auf der Grundlage von Werten zu berechnen, die aus der Berechnung von Elementen mit einem höheren Wert abgeleitet sind. Wird ein berechnetes Element ohne das **SOLVE_ORDER** -Schlüsselwort definiert, lautet sein Standardwert 0.  
  
 Wenn Sie beispielsweise die in den ersten beiden Beispielabfragen verwendeten Berechnungen kombinieren, überschneiden sich die beiden berechneten Elemente `Year Difference` und `Profit Margin`in einer einzelnen Zelle im Resultdataset der MDX-Beispielabfrage. Nur anhand der Lösungsreihenfolge lässt sich bestimmen, wie [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] diese Zelle auswertet. Die Formeln, mit denen diese Zelle erstellt wird, erzeugen je nach Lösungsreihenfolge der beiden berechneten Elemente unterschiedliche Ergebnisse.  
  
 Versuchen Sie zunächst, die in den ersten beiden Abfragen verwendeten Berechnungen in der folgenden MDX-Abfrage zu kombinieren:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 In diesem Beispiel für eine kombinierte MDX-Abfrage weist `Profit Margin` die höchste Lösungsreihenfolge auf und hat daher bei der Interaktion zweier Ausdrücke Vorrang. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] wertet die betreffende Zelle mit der `Profit Margin` -Formel aus. Das Ergebnis dieser geschachtelten Berechnung ist in der folgenden Tabelle dargestellt.  
  
||Internet Sales Amount|Internet Total Product Cost|Profit Margin|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**KJ 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|114.28%|  
  
 Das Ergebnis in der freigegebenen Zelle basiert auf der Formel für `Profit Margin`. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] berechnet also das Ergebnis in der freigegebenen Zelle mit den `Year Difference` -Daten, wodurch folgende Formel erzeugt wird (das Ergebnis wurde zur besseren Übersicht gerundet):  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 oder  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 Dies ist eindeutig falsch. Wenn die Lösungsreihenfolge für die berechneten Elemente in der MDX-Abfrage vertauscht wird, berechnet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] das Ergebnis in der freigegebenen Zelle jedoch anders. Mit der folgenden kombinierten MDX-Abfrage wird die Lösungsreihenfolge für berechnete Elemente umgekehrt:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Da die Reihenfolge der berechneten Elemente vertauscht wurde, verwendet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zum Auswerten der Zelle die `Year Difference` -Formel, wie in der folgenden Tabelle gezeigt.  
  
||Internet Sales Amount|Internet Total Product Cost|Profit Margin|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**KJ 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|(0.15%)|  
  
 Da in dieser Abfrage die `Year Difference` -Formel mit den Daten für `Profit Margin` verwendet wird, gleicht die Formel für die freigegebene Zelle der folgenden Berechnung:  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 oder  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>Weitere Überlegungen  
 Die Lösungsreihenfolge kann ein sehr komplexes Problem darstellen, besonders in Cubes mit einer hohen Anzahl von Dimensionen, die berechnete Elemente, benutzerdefinierte Rollupformeln oder berechnete Zellen beinhalten. Wenn [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] eine MDX-Abfrage auswertet, berücksichtigt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] die Werte der Lösungsreihenfolge für alle Teile in einem bestimmten Durchlauf, einschließlich der Dimensionen des in der MDX-Abfrage angegebenen Cubes.  
  
## <a name="see-also"></a>Siehe auch  
 [CalculationCurrentPass &#40;MDX&#41;](../../../mdx/calculationcurrentpass-mdx.md)   
 [CalculationPassValue &#40; MDX &#41;](../../../mdx/calculationpassvalue-mdx.md)   
 [CREATE MEMBER-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Bearbeiten von Daten &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
