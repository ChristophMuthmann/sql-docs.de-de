---
title: Sichtbare Gesamtwerte und nicht sichtbare Gesamtwerte | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea9d02f2-a668-4547-ade5-e3d077a2e1bd
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d85d2ce789793c03fa99d51451e1a64d0868962
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="visual-totals-and-non-visual-totals"></a>Sichtbare Gesamtwerte und nicht sichtbare Gesamtwerte
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Als sichtbare Gesamtwerte werden Gesamtbeträge am Ende einer Spalte oder Zeile bezeichnet, in denen alle in der Spalte bzw. Zeile sichtbaren Elemente zusammengezählt wurden. Dies ist bei der Anzeige der meisten Tabellen das Standardverhalten. In bestimmten Fällen sollen jedoch möglicherweise nur bestimmte Spalten in einer Tabelle, jedoch die Gesamtbeträge für die komplette Zeile angezeigt werden, einschließlich der nicht sichtbaren Spalten. Diese werden als **nicht sichtbare Gesamtwerte**bezeichnet, da der Gesamtbetrag sowohl die sichtbaren als auch die nicht sichtbaren Werte umfasst.  
  
 Das folgende Szenario veranschaulicht das Verhalten von nicht sichtbaren Gesamtwerten. Der erste Schritt zeigt das Standardverhalten von sichtbaren Gesamtwerten.  
  
 Das nachfolgende Beispiel zeigt eine [Adventure Works]-Abfrage, um Werte zu [Reseller Sales Amount] in einer Tabelle abzurufen, wobei die Produktkategorien die Spalten und die Geschäftstypen der Wiederverkäufer die Zeilen sind. Beachten Sie, dass sowohl für Produkte als auch für Wiederverkäufer Gesamtbeträge angegeben werden, wenn die folgende SELECT-Anweisung ausgegeben wird:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Hierdurch werden folgende Ergebnisse erzielt:  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Fahrräder**|**Bekleidung**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
## <a name="non-visual-on-rows-and-columns"></a>Nicht sichtbare Gesamtwerte für Zeilen und Spalten  
 Wenn Sie eine Tabelle erstellen möchten, die nur Accessories- und Clothing-Produkte sowie Wiederverkäufer vom Typ Value Added Reseller und Warehouse enthält, wobei die Gesamtbeträge jedoch beibehalten werden, können Sie die folgende Anweisung mit NON VISUAL ausgeben:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Hierdurch werden folgende Ergebnisse erzielt:  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
## <a name="non-visual-on-rows"></a>Nicht sichtbare Gesamtwerte für Zeilen  
 Wenn Sie eine Tabelle erstellen möchten, in der sichtbare Gesamtwerte für die Spalten, für die Zeilensummen jedoch die tatsächliche Summe aller [Category]-Werten angezeigt werden, geben Sie die folgende Abfrage aus:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 NON VISUAL wird nur auf [Category] angewendet.  
  
 Die oben dargestellte Abfrage führt zu den folgenden Ergebnissen:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Im Vergleich zu den vorhergehenden Ergebnissen können Sie feststellen, dass die Zeile [All Resellers] jetzt die Summe der angezeigten Werte für [Value Added Reseller] und [Warehouse] enthält, die Spalte [All Products] hingegen den Gesamtwert aller Produkte anzeigt, einschließlich der nicht sichtbaren Produkte.  
  
## <a name="see-also"></a>Siehe auch  
 [Schlüsselkonzepte in MDX &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Arbeiten mit Elemente, Tupel und Mengen &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Grundlegendes zu MDX-Abfrage &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Grundlegende MDX-Abfrage &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Beschränken die Abfrage mit Abfrage- und Slicerachsen &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)   
 [Des Cubekontexts in einer Abfrage &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)  
  
  
