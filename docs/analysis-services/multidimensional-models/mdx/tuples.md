---
title: Tupel | Microsoft Docs
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
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 00353a4a955b631fda3e0fb6521ecad764f1328c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="tuples"></a>Tupel
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Ein Tupel dient zur eindeutigen Identifizierung eines Slices von Daten aus einem Cube. Das Tupel wird durch eine Kombination aus Dimensionselementen gebildet, sofern nicht zwei oder mehr Elemente zur gleichen Hierarchie gehören.  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>Implizite oder Standardattributelemente in einem Tupel  
 Zum Definieren eines Tupels in einer MDX-Abfrage oder in einem MDX-Ausdruck ist es nicht erforderlich, die Attributelemente aus allen Attributhierarchien explizit einzuschließen. Wenn ein Element aus einer Attributhierarchie nicht explizit in eine Abfrage oder einen Ausdruck eingeschlossen ist, wird das Standardelement der betreffenden Attributhierarchie implizit in das Tupel eingeschlossen. Sofern nicht anderweitig explizit in einem Cube definiert, ist das Standardelement jeder Attributhierarchie das (Alle)-Element, falls ein solches vorhanden ist. Wenn kein (Alle)-Element innerhalb einer Attributhierarchie vorhanden ist, wird als Standardelement ein Element der obersten Ebene der Attributhierarchie verwendet. Sofern kein anderes Standardmeasure explizit definiert wurde, wird als Standardmeasure das erste im Cube angegebene Measure verwendet. Weitere Informationen finden Sie unter [Definieren eines Standardelements](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md) und [DefaultMember &#40;MDX&#41;](../../../mdx/defaultmember-mdx.md).  
  
 Beispielsweise identifiziert das folgende Tupel eine einzelne Zelle in der Adventure Works-Datenbank, wobei nur ein einziges Element der Measuredimension explizit definiert ist.  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 Im vorherigen Beispiel wurde die Zelle eindeutig identifiziert, die das Reseller Sales Amount-Element der Measure-Dimension und das Standardelement jeder Attributhierarchie im Cube enthält. Das Standardelement jeder Attributhierarchie ist dabei das jeweilige (Alle)-Element. Eine Ausnahme stellt die Destination Currency-Attributhierarchie dar. Das Standardelement der Destination Currency-Hierarchie ist das US Dollar-Element (dieses Standardelement ist im MDX-Skript des Adventure Works-Cube definiert).  
  
> [!IMPORTANT]  
>  Das Element einer Attributhierarchie in einem Tupel wird auch von den Beziehungen beeinflusst, die zwischen Attributen innerhalb einer Dimension definiert sind.  
  
 Die folgende Abfrage gibt den Wert der Zelle zurück, auf die sich das im vorherigen Beispiel angegebene Tupel bezog ($80,450.596.98).  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Wenn Sie in einer Abfrage eine Achse für eine Menge angeben (in diesem Fall bestehend aus einem einzigen Tupel), müssen Sie zunächst eine Menge für die Spaltenachse und dann eine Menge für die Zeilenachse angeben. Die Spaltenachse wird auch als *axis(0)* oder einfach *0* bezeichnet. Weitere Informationen zu MDX-Abfragen finden Sie unter [Die grundlegende MDX-Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md).  
  
### <a name="tuples-as-values-or-member-references"></a>Tupel als Werte oder Elementverweise  
 Wie das vorherige Beispiel zeigte, können Sie ein Tupel in einer Abfrage verwenden, um den Wert in der Zelle zurückzugeben, auf die das Tupel verweist. Sie können ein Tupel aber auch in einem Ausdruck verwenden, um explizit auf das im Tupel angegebene Element zu verweisen. Abfragen und Ausdrücke können mithilfe von Funktionen Tupel zurückgeben oder verarbeiten. Mit einem Tupel kann entweder auf den Wert einer Zelle, die das Tupel angibt, verwiesen werden oder, bei Verwendung in einer Funktion, eine Kombination von Elementen angegeben werden.  
  
### <a name="tuple-dimensionality"></a>Tupeldimensionalität  
 Mit *Dimensionalität* eines Tupels ist die Sequenz oder Reihenfolge der Elemente im Tupel gemeint. Da implizite Elemente immer in der gleichen Reihenfolge auftreten, bezieht sich der Begriff Dimensionalität meistens ausschließlich auf die explizit definierten Elemente eines Tupels. Die Reihenfolge der Elemente eines Tupels ist beim Definieren einer Menge von Tupeln von großer Bedeutung. Im folgenden Beispiel werden zwei Elemente in ein Tupel auf der Spaltenachse eingeschlossen.  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Wenn Sie in einem Tupel Elemente aus mehreren Dimensionen explizit angeben, müssen Sie das gesamte Tupel in Klammern einschließen. Wenn Sie nur ein einziges Element in einem Tupel angeben, sind die Klammern optional.  
  
 Das Tupel in der Abfrage aus dem vorherigen Beispiel gibt den Rückgabewert der Cubezelle an, die sich am Schnittpunkt des Reseller Sales Amount-Measures der Measure-Dimension mit dem CY 2004-Element der Calendar Year-Attributhierarchie in der Date-Dimension befindet.  
  
> [!NOTE]  
>  Auf ein Attributelement kann entweder mit seinem Elementnamen oder seinem Elementschlüssel verwiesen werden. Der Verweis auf [CY 2004] im vorherigen Beispiel könnte durch &[2004] ersetzt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Schlüsselkonzepte in MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Cuberaum](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Arbeiten mit Elemente, Tupel und Mengen &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)  
  
  
