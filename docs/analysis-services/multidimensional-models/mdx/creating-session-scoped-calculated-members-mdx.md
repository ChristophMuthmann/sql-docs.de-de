---
title: "Erstellen berechneter Elemente im Bereich einer Sitzung (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CREATE MEMBER-Anweisung"
  - "Berechnete Elemente im Bereich einer Sitzung [MDX]"
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Erstellen berechneter Elemente im Bereich einer Sitzung (MDX)
  Zum Erstellen eines berechneten Elements, das während einer gesamten MDX-Sitzung (Multidimensional Expressions) verfügbar ist, verwenden Sie die [CREATE MEMBER](../Topic/CREATE%20MEMBER%20Statement%20\(MDX\).md)-Anweisung. Ein berechnetes Element, das mit der CREATE MEMBER-Anweisung erstellt wurde, wird erst entfernt, nachdem die MDX-Sitzung geschlossen wurde.  
  
 Wie in diesem Thema erläutert wird, ist die Syntax der CREATE MEMBER-Anweisung unkompliziert und einfach zu verwenden.  
  
> [!NOTE]  
>  Weitere Informationen zu berechneten Elementen finden Sie unter [Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md).  
  
## Syntax von CREATE MEMBER  
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
  
## Beispiel zu CREATE MEMBER  
 Im folgenden Beispiel wird die CREATE MEMBER-Anweisung dazu verwendet, das berechnete Element `LastFourStores` zu erstellen. Dieses berechnete Element gibt die Summe der verkauften Einheiten für die letzten vier Filialen zurück und ist während der gesamten Cubesitzung verfügbar.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## Siehe auch  
 [Erstellen berechneter Elemente im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-calculated-members-mdx.md)  
  
  