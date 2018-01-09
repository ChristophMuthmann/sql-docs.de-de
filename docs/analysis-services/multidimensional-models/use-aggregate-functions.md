---
title: Verwenden von Aggregatfunktionen | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: aggregate functions [Analysis Services]
ms.assetid: c42166ef-b75c-45f4-859c-09a3e9617664
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b22f964bbc9659187cf67320951b75d93cb89331
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="use-aggregate-functions"></a>Verwenden von Aggregatfunktionen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn eine Dimension zum Segmentieren eines Measures verwendet wird, wird das Measure gemäß den in dieser Dimension enthaltenen Hierarchien zusammengefasst. Das Zusammenfassungsverhalten hängt von der für das Measure angegebenen Aggregatfunktion ab. Für die meisten Measures, die numerische Daten enthalten, ist die Aggregatfunktion **Sum**. Der Wert des Measures wird je nach de Ebene, auf der die Hierarchie aktiv ist, zu unterschiedlichen Mengen summiert.  
  
 In Analysis Services wird jedes Measure, das Sie erstellen, durch eine Aggregationsfunktion gesichert, die den Betrieb des Measures bestimmt. Zu den vordefinierten Aggregationstypen zählen **Sum**, **Min**, **Max**, **Count**, **Distinct Count**und einige andere, spezialisiertere Funktionen. Wenn Sie Aggregationen basierend auf komplexen oder benutzerdefinierten Formeln benötigen, können Sie alternativ eine MDX-Berechnung anstelle einer vorgefertigten Aggregationsfunktion erstellen. Wenn Sie beispielsweise ein Measure für einen Prozentwert definieren möchten, würden Sie dies in MDX anhand eines berechneten Measures tun. Siehe [CREATE MEMBER-Anweisung &#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md).  
  
 Measures, die über den Cube-Assistenten erstellt werden, wird als Teil der Measuredefinition ein Aggregationstyp zugewiesen. Der Aggregationstyp ist immer **Sum**, sofern die Quellspalte numerische Daten enthält. **Sum** wird unabhängig vom Datentyp der Quellspalte zugewiesen. Wenn Sie beispielsweise den Cube-Assistenten zum Erstellen von Measures verwendet und alle Spalten aus einer Faktentabelle abgerufen haben, werden Sie feststellen, dass alle sich daraus ergebenden Measures eine Aggregation von **Sum**aufweisen, selbst wenn die Quelle eine Datums-/Zeitspalte ist. Überprüfen Sie immer die vorab zugeordneten Aggregationsmethoden für Measures, die über den Assistenten erstellt wurden, um sicherzustellen, dass die Aggregationsfunktion geeignet ist.  
  
 Sie können die Aggregationsmethode in der Cubedefinition über [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]oder über MDX zuweisen oder ändern. Weitere Informationen finden Sie unter [Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) oder [Aggregat &#40;MDX&#41;](../../mdx/aggregate-mdx.md).  
  
##  <a name="AggFunction"></a> Aggregatfunktionen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt Funktionen zur Verfügung, um Measures über die Dimensionen in Measuregruppen zu aggregieren. Die *Additivität* einer Aggregationsfunktion legt fest, wie das Measure über alle Dimensionen im Cube hinweg aggregiert wird. Aggregationsfunktionen werden nach drei Ebenen der Additivität unterschieden:  
  
 Additiv  
 Ein additives Measure, auch als vollständig additives Measure bezeichnet, kann über alle Dimensionen hinweg innerhalb der Measuregruppe, die das Measure enthält, uneingeschränkt aggregiert werden.  
  
 Semiadditiv  
 Ein semiadditives Measure kann über eine oder mehrere, jedoch nicht alle Dimensionen hinweg in der Measuregruppe, die das Measure enthält, aggregiert werden. So kann beispielsweise ein Measure, das die Menge des Lagerbestands darstellt, über eine geografische Dimension aggregiert werden und ergibt so eine Gesamtmenge, die allen Warenlagern zur Verfügung steht. Das Measure kann jedoch nicht über eine Zeitdimension aggregiert werden, da das Measure eine regelmäßig erstellte Momentaufnahme der verfügbaren Mengen darstellt. Die Aggregation eines solchen Measures über eine Zeitdimension würde zu falschen Ergebnissen führen. Einzelheiten dazu finden Sie unter [Define Semiadditive Behavior](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md) .  
  
 Nicht additiv  
 Ein nicht additives Measure kann nicht über Dimensionen hinweg in der Measuregruppe, die das Measure enthält, aggregiert werden. Anstelle dessen muss das Measure einzeln für jede Zelle im Cube, die das Measure darstellt, berechnet werden. So kann beispielsweise ein berechnetes Measure, das einen Prozentwert zurückgibt, z. B. die Bruttorendite, nicht von den Prozentwerten der untergeordneten Elemente in den Dimensionen aggregiert werden.  
  
 In der folgenden Tabelle werden die Aggregationsfunktionen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]aufgelistet und sowohl die Additivität als auch das erwartete Ergebnis der Funktion beschrieben.  
  
|Aggregationsfunktion|Additivität|Rückgabewert|  
|--------------------------|----------------|--------------------|  
|**Sum**|Additiv|Berechnet die Summe der Werte für alle untergeordneten Elemente. Dies ist die Standardaggregationsfunktion.|  
|**Count**|Additiv|Ruft die Zahl aller untergeordneten Elemente ab.|  
|**Min**|Semiadditiv|Ruft den niedrigsten Wert für alle untergeordneten Elemente ab.|  
|**Max**|Semiadditiv|Ruft den höchsten Wert für alle untergeordneten Elemente ab.|  
|**DistinctCount**|Nicht additiv|Ruft die Zahl aller eindeutigen untergeordneten Elemente ab. Weitere Informationen finden Sie unter [About Distinct Count Measures](../../analysis-services/multidimensional-models/use-aggregate-functions.md#bkmk_distinct) im nächsten Abschnitt.|  
|**Keine**|Nicht additiv|Es wird keine Aggregation durchgeführt. Alle Werte für Blatt- und Nichtblattelemente in einer Dimension werden direkt von der Faktentabelle für die Measuregruppe bereitgestellt, die das Measure enthält. Wenn kein Wert aus der Faktentabelle für ein Element gelesen werden kann, wird der Wert für dieses Element auf NULL gesetzt.|  
|**ByAccount**|Semiadditiv|Berechnet die Aggregation gemäß der Aggregationsfunktion, die dem Kontotyp eines Elements in einer Kontodimension zugewiesen ist. Ist keine Kontodimension in der Measuregruppe vorhanden, wird der Wert als **None** -Aggregationsfunktion behandelt.<br /><br /> Weitere Informationen zu Kontodimensionen finden Sie unter [Erstellen eines Finanzkontos des über- und untergeordneten Typs Dimension](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|**AverageOfChildren**|Semiadditiv|Berechnet den Durchschnitt der Werte für alle nicht leeren, untergeordneten Elemente.|  
|**FirstChild**|Semiadditiv|Ruft den Wert des ersten untergeordneten Elements ab.|  
|**LastChild**|Semiadditiv|Ruft den Wert des letzten untergeordneten Elements ab.|  
|**FirstNonEmpty**|Semiadditiv|Ruft den Wert des ersten nicht leeren untergeordneten Elements ab.|  
|**LastNonEmpty**|Semiadditiv|Ruft den Wert des letzten nicht leeren untergeordneten Elements ab.|  
  
##  <a name="bkmk_distinct"></a> About Distinct Count Measures  
 Ein Measure mit dem **Aggregate-Funktion** -Eigenschaftswert **Distinct Count** wird als "Distinct Count Measure" bezeichnet. Ein Distinct Count Measure kann verwendet werden, um die Vorkommen der Elemente der untersten Ebene einer Dimension in der Faktentabelle zu zählen. Da nur unterschiedliche Elemente gezählt werden, wird ein mehrfach auftretendes Element nur einmal gezählt. Ein Distinct Count-Measure wird immer in einer speziellen Measuregruppe platziert. Das Einfügen eines Distinct Count-Measures in seine eigene Measuregruppe ist eine bewährte Methode, die zur Leistungsoptimierung in den Designer integriert wurde.  
  
 Distinct Count Measures werden im Allgemeinen dazu verwendet, für jedes Element einer Dimension zu bestimmen, wie viele unterschiedliche Elemente der untersten Ebene einer anderen Dimension Zeilen der Faktentabelle gemeinsam nutzen. Beispielsweise wird in einem Sales-Cube bestimmt, wie viele unterschiedliche Produkte von den einzelnen Kunden und Kundengruppen gekauft wurden. (Auf die einzelnen Elemente der Customers-Dimension bezogen bedeutet das: Von wie vielen unterschiedlichen Elementen der untersten Ebene der Products-Dimension werden Zeilen der Faktentabelle gemeinsam genutzt?) Ein weiteres Beispiel: In einem Cube für die Zählung der Besucher einer Internetsite wird pro Sitebesucher und Sitebesuchergruppe bestimmt, wie viele unterschiedliche Seiten der Internetsite besucht wurden. (Auf die einzelnen Elemente der Site Visitors-Dimension bezogen bedeutet das: Von wie vielen unterschiedlichen Elementen der untersten Ebene der Pages-Dimension werden Zeilen der Faktentabelle gemeinsam genutzt?) In jedem dieser Beispiele werden die Elemente der untersten Ebene der zweiten Dimension über ein Distinct Count Measure gezählt.  
  
 Diese Art von Analyse ist nicht auf zwei Dimensionen beschränkt. Tatsächlich kann ein Distinct Count Measure getrennt und nach einer beliebigen Kombination von Dimensionen des Cubes in Slices aufgeteilt werden, einschließlich der Dimension, die die gezählten Elemente enthält.  
  
 Ein Distinct Count Measure, das zur Zählung von Elementen dient, basiert auf einer Fremdschlüsselspalte der Faktentabelle. (Das heißt, dass die **Source Column**-Eigenschaft des Measures diese Spalte identifiziert.) Diese Spalte verknüpft die Dimensionstabellenspalte, die die über das Distinct Count Measure gezählten Elemente identifiziert.  
  
## <a name="see-also"></a>Siehe auch  
 [Measures und Measuregruppen](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../../mdx/mdx-function-reference-mdx.md)   
 [Definieren des semiadditiven Verhaltens](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)  
  
  
