---
title: Erstellen im Bereich einer Sitzung berechnete Elemente (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- CREATE MEMBER statement
- session-scoped calculated members [MDX]
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b922b07e830c7cf87345e434f6667e5b0e53a82
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>MDX berechnete Elemente - Bereich einer Sitzung berechnete Elemente
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Um ein berechnetes Element erstellen, die in der gesamten Sitzung MDX (Multidimensional Expressions) verfügbar ist, verwenden Sie die [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md) Anweisung. Ein berechnetes Element, das mit der CREATE MEMBER-Anweisung erstellt wurde, wird erst entfernt, nachdem die MDX-Sitzung geschlossen wurde.  
  
 Wie in diesem Thema erläutert wird, ist die Syntax der CREATE MEMBER-Anweisung unkompliziert und einfach zu verwenden.  
  
> [!NOTE]  
>  Weitere Informationen zu berechneten Elementen finden Sie unter [Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
## <a name="create-member-syntax"></a>Syntax von CREATE MEMBER  
 Verwenden Sie die folgende Syntax, um der MDX-Anweisung die CREATE MEMBER-Anweisung hinzuzufügen:  
  
```  
CREATE [SESSION] MEMBER [<cube-name>.]<fully-qualified-member-name> AS <expression> [,<property-definition-list>]  
<cube name> ::= CURRENTCUBE | <Cube Name>  
<property-definition-list> ::= <property-definition>  
  | <property-definition>, <property-definition-list>  
<property-definition> ::= <property-identifier> = <property-value>  
<property-identifier> ::= VISIBLE | SOLVEORDER | SOLVE_ORDER | FORMAT_STRING | NON_EMPTY_BEHAVIOR <ole db member properties>  
```  
  
 In der Syntax für die CREATE MEMBER-Anweisung entspricht der `fully-qualified-member-name` -Wert dem vollqualifizierten Namen des berechneten Elements. Der vollqualifizierte Name enthält die Dimension oder Ebene, der das berechnete Element zugeordnet ist. Der `expression` -Wert gibt den Wert des berechneten Elements zurück, nachdem der Wert des Ausdrucks ausgewertet wurde.  
  
## <a name="create-member-example"></a>Beispiel zu CREATE MEMBER  
 Im folgenden Beispiel wird die CREATE MEMBER-Anweisung dazu verwendet, das berechnete Element `LastFourStores` zu erstellen. Dieses berechnete Element gibt die Summe der verkauften Einheiten für die letzten vier Filialen zurück und ist während der gesamten Cubesitzung verfügbar.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen berechneter Elemente im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
