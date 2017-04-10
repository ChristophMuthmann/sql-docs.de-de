---
title: "Grundlegendes MDX-Skript (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "MDX-Standardskripts"
  - "Anweisungen [MDX]"
  - "Ausdrücke [MDX], Skripts"
  - "Skripts [MDX], Informationen zu Skripts"
ms.assetid: 83d9afda-7d34-42b5-8f28-20172a905f23
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Grundlegendes MDX-Skript (MDX)
  Ein MDX-Skript (Multidimensional Expressions, mehrdimensionale Ausdrücke) definiert den Berechnungsprozess für einen Cube in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Es gibt zwei Arten von MDX-Skripts:  
  
 **Das MDX-Standardskript**  
 In dem Moment, in dem Sie einen Cube erstellen, erstellt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ein MDX-Standardskript für den Cube. In diesem Skript ist ein Berechnungsdurchlauf für den gesamten Cube definiert.  
  
 **Benutzerdefiniertes MDX-Skript**  
 Nachdem Sie einen Cube erstellt haben, können Sie benutzerdefinierte MDX-Skripts hinzufügen, um die Berechnungsmöglichkeiten für den Cube zu erweitern.  
  
## Das MDX-Standardskript  
 Das MDX-Standardskript, das [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] erstellt, wenn Sie einen Cube definieren, enthält eine einzige CALCULATE-Anweisung. Diese einzige CALCULATE-Anweisung befindet sich am Anfang des MDX-Standardskripts und gibt an, dass beim ersten Berechnungsdurchlauf der gesamte Cube berechnet werden soll.  
  
 Das MDX-Standardskript enthält außerdem die Skriptbefehle, die benannte Mengen, Zuweisungen und berechnete Elemente erstellen, die im Cube-Designer erstellt wurden:  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] fügt dem MDX-Standardskript Skriptbefehle direkt hinzu.  
  
-   Für jede benannte Menge im Cube gibt es im MDX-Standardskript eine entsprechende CREATE SET-Anweisung.  
  
-   Für jedes berechnete Element, das im Cube definiert ist, gibt es im MDX-Standardskript eine entsprechende CREATE MEMBER-Anweisung.  
  
 Die Reihenfolge, die die Skriptbefehle, benannten Mengen und berechneten Elemente im MDX-Standardskript haben, können Sie im Cube-Designer über die Registerkarte **Berechnungen** festlegen. Weitere Informationen zum Definieren von Berechnungen, die im MDX-Standardskript gespeichert werden, finden Sie unter [Berechnungen in mehrdimensionalen Modellen](../../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md).  
  
 Ist einem Cube kein MDX-Skript zugeordnet, nimmt der Cube das MDX-Standardskript an. Einem Cube muss mindestens ein MDX-Skript zugeordnet sein, weil ein Cube anhand des MDX-Skripts das Berechnungsverhalten ermittelt. Dies bedeutet, dass ein Cube, dem kein oder ein leeres MDX-Skript zugeordnet wurde, keine Zellen berechnen kann. Wenn Sie Cubes programmgesteuert erstellen, entweder mit ASSL-Befehlen (Analysis Services Scripting Language) oder mit Analysis Management Objects (AMO), empfiehlt es sich, dass Sie ein MDX-Standardskript erstellen, das eine einzige CALCULATE-Anweisung für den Cube enthält.  
  
## Inhalt eines MDX-Skripts  
 Ein MDX-Skript kann die folgenden Anweisungen und Ausdrücke enthalten:  
  
 Alle MDX-Skriptanweisungen  
 In einem MDX-Skript steuern MDX-Skriptbefehle den Kontext und den Gültigkeitsbereich von Berechnungen und verwalten das Verhalten anderer Anweisungen im MDX-Skript. Zu dieser Kategorie gehören die folgenden Anweisungen:  
  
-   [CALCULATE](../Topic/CALCULATE%20Statement%20\(MDX\).md)  
  
-   [FREEZE](../Topic/FREEZE%20Statement%20\(MDX\).md)  
  
-   [SCOPE](../Topic/SCOPE%20Statement%20\(MDX\).md)  
  
 Weitere Informationen zu MDX-Skriptanweisungen finden Sie unter [MDX-Skriptanweisungen &#40;MDX&#41;](../../../mdx/mdx-scripting-statements-mdx.md).  
  
 [CREATE MEMBER](../Topic/CREATE%20MEMBER%20Statement%20\(MDX\).md)  
 Die CREATE MEMBER-Anweisung erstellt berechnete Elemente. Weitere Informationen zum Erstellen berechneter Elemente finden Sie unter [Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md).  
  
 [CREATE SET](../Topic/CREATE%20SET%20Statement%20\(MDX\).md)  
 Die CREATE SET-Anweisung erstellt benannte Mengen. Weitere Informationen zum Erstellen von benannten Mengen finden Sie unter [Erstellen von benannten Mengen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md).  
  
 Bedingte Anweisungen  
 Bedingte Anweisungen erweitern MDX-Skripts um logische Befehle mit Bedingungen. Zu dieser Kategorie gehören die Anweisungen [CASE](../../../mdx/case-statement-mdx.md) und [IF](../Topic/IF%20Statement%20%20\(MDX\).md) .  
  
 Zuweisungsausdrücke  
 Ein Zuweisungsausdruck weist einem eingeschränkten Teilcube einen Ausdruck (z. B. einen Wert) zu. Ein eingeschränkter Teilcubeausdruck ist eine Auflistung eingeschränkter Mengenausdrücke, die in einem MDX-Skript die "Kanten" eines Teilcubes definieren. Der folgende Code zeigt die Syntax für einen eingeschränkten Teilcubeausdruck:  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## Siehe auch  
 [MDX-Sprachreferenz &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  