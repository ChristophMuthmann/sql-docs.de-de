---
title: Abfragen von mehrdimensionalen Daten mit MDX | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31dd33f2edaf44c9d6ff5a14c6a5a54cd6edfda7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="querying-multidimensional-data-with-mdx"></a>Abfragen von mehrdimensionalen Daten mit MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX (Multidimensional Expressions) ist eine Abfragesprache zum Verwenden und Abrufen von mehrdimensionalen Daten in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. MDX basiert auf der XMLA-Spezifikation (XML for Analysis) und verfügt über spezielle Erweiterungen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. MDX verwendet Ausdrücke bestehend aus Bezeichnern, Werten, Anweisungen, Funktionen und Operatoren, die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zum Abrufen von Objekten (z. B. einer Menge oder einem Element) oder Skalarwerten (z. B. einer Zeichenfolge oder einer Zahl) auswerten kann.  
  
 MDX-Abfragen und -Ausdrücke werden in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] für folgende Zwecke verwendet:  
  
-   Zurückgeben von Daten aus einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Cube an eine Clientanwendung  
  
-   Formatieren von Abfrageergebnissen  
  
-   Ausführen von Cube-Entwurfsaufgaben, wie z. B. Definieren von berechneten Elementen, benannten Mengen, Zuweisungen mit definiertem Bereich oder Key Performance Indicators (KPI)  
  
-   Ausführen von Verwaltungsaufgaben, wie z. B. Dimensions- und Zellensicherheit  
  
 Die MDX-Syntax ist, oberflächlich betrachtet, der SQL-Syntax sehr ähnlich, die normalerweise bei relationalen Datenbanken verwendet wird. MDX ist jedoch keine Erweiterung von SQL und unterscheidet sich in vielerlei Hinsicht von SQL. Um MDX-Ausdrücke zum Entwerfen bzw. Sichern von Cubes oder MDX-Abfragen zum Zurückgeben und Formatieren von mehrdimensionalen Daten erstellen zu können, müssen Sie die grundlegenden Konzepte von MDX und der Dimensionsmodellierung, die MDX-Syntaxelemente, MDX-Operatoren, MDX-Anweisungen sowie MDX-Funktionen verstehen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Schlüsselkonzepte in MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)|Mithilfe von MDX (Multidimensional Expressions) können Sie mehrdimensionale Daten abfragen oder MDX-Ausdrücke zur Verwendung innerhalb eines Cubes erstellen. Voraussetzung dafür ist jedoch, dass Sie über Grundkenntnisse der Dimensionskonzepte und Terminologie von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verfügen.|  
|[Grundlegendes zu MDX-Abfrage & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)|MDX (Multidimensional Expressions) ermöglicht Ihnen das Abfragen von mehrdimensionalen Objekten (z. B. Cubes) sowie das Zurückgeben von mehrdimensionalen Cellsets, die die Daten des jeweiligen Cubes enthalten. Dieses Thema und die zugehörigen Unterthemen bieten eine Übersicht über MDX-Abfragen.|  
|[Grundlegendes zu MDX-Skripts & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)|In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] besteht ein MDX-Skript (Multidimensional Expressions) aus einem oder mehreren MDX-Ausdrücken oder -Anweisungen, die einen Cube mit Berechnungen auffüllen.<br /><br /> In einem MDX-Skript wird der Berechnungsprozess für einen Cube definiert. Ein MDX-Skript wird auch als Teil des Cubes selbst angesehen. Daher bewirkt ein Ändern eines MDX-Skripts, das einem Cube zugeordnet ist, dass der Berechnungsprozess für den Cube sofort geändert wird.<br /><br /> Um MDX-Skripts zu erstellen, können Sie den Cube-Designer in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]verwenden.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Syntaxelemente & #40; MDX & #41;](../../../mdx/mdx-syntax-elements-mdx.md)   
 [MDX-Sprachreferenz & #40; MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  
