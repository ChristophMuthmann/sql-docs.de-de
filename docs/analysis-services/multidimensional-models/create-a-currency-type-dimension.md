---
title: "Erstellen einer W&#228;hrungstypdimension | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dimensionen [Analysis Services], Währung"
  - "Währung [Analysis Services]"
  - "Umrechnen von Währungen"
  - "Währungsdimensionen [Analysis Services]"
ms.assetid: b1f037d1-ce47-4e47-a1c2-5ec9e781cff6
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Erstellen einer W&#228;hrungstypdimension
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist eine Dimension vom Typ "Währung" eine Dimension, deren Attribute eine Auflistung von Währungen für Finanzberichte darstellt.  
  
 Mit einer Währungsdimension können Sie einem Cube in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Funktionen für die Währungsumrechnung hinzufügen. Wenn Sie einem Cube die Währungsumrechnung hinzufügen möchten, verwenden Sie den Business Intelligence-Assistenten zum Definieren eines Multidimensional Expressions-(MDX-)Skriptbefehls, der Währungsmeasures in Werte konvertiert, die für das Gebietsschema der Clientanwendung geeignet sind. Um dieses MDX-Skript erstellen zu können, benötigt der Business Intelligence-Assistent folgende Informationen:  
  
-   Eine Währungsdimension, die Quellwährungen darstellt. (Bei dieser Dimension handelt es sich um die Quellwährungsdimension.)  
  
-   Eine Measuregruppe, die die zu verwendenden Wechselkurse darstellt.  
  
 Anhand dieser Informationen entwirft der Business Intelligence-Assistent einen Währungsumrechnungsprozess, der die entsprechende Zielwährungsdimension (die Währungsdimension, die Zielwährungen darstellt) identifiziert. Abhängig von der Anzahl der Währungsumrechnungen, die für Ihre Business Intelligence-Lösung erforderlich sind, kann der Business Intelligence-Assistent mehrere Zielwährungsdimensionen definieren. Weitere Informationen zum Definieren von Währungsumrechnungen finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).  
  
 Wenn Sie eine Dimension als Währungsdimension identifizieren möchten, legen Sie die **Type** -Eigenschaft der Dimension auf **Currency**fest.  
  
## Dimensionsstruktur  
 Eine Währungsdimension enthält zumindest ein Schlüsselattribut, das die einzelnen Währungen in der Dimensionstabelle für die Währungsdimension identifiziert. Der Wert des Schlüsselattributs ist in Quell- und Zielwährungsdimensionen unterschiedlich.  
  
-   Wenn Sie ein Attribut als Schlüsselattribut einer Quellwährungsdimension identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencySource**fest.  
  
-   Wenn Sie ein Attribut als Zielwährungsdimension identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencyDestination**fest.  
  
 Für Berichtszwecke enthalten sowohl Quell- als auch Zielwährungsdimensionen optional folgende Attribute:  
  
-   Ein Attribut für den Namen der Währung.  
  
     Wenn Sie ein Attribut als Attribut für den Namen der Währung identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencyName**fest.  
  
-   Ein Attribut für die Quelle der Währung.  
  
     Wenn Sie ein Attribut als Attribut für die Quelle der Währung identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencySource**fest.  
  
-   Einen Währungscode gemäß der International Standards Organization (ISO).  
  
     Wenn Sie ein Attribut als Attribut für den ISO-Währungscode identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencyIsoCode**fest.  
  
 Weitere Informationen zu Attributtypen finden Sie unter [Konfigurieren von Attributtypen](../../analysis-services/multidimensional-models/configure-attribute-types.md).  
  
## Definieren von Kontointelligenz mit dem Business Intelligence-Assistenten  
 Nachdem Sie eine Kontodimension definiert und diese Dimension einem Cube hinzugefügt haben, können Sie den Business Intelligence-Assistenten verwenden, um der Dimension die Kontointelligenzfunktionalität hinzuzufügen, beispielsweise das Identifizieren und Zuordnen von Kontotypen. Weitere Informationen finden Sie unter [Hinzufügen von Kontointelligenz zu einer Dimension](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Business Intelligence-Assistent (F1-Hilfe)](../Topic/Business%20Intelligence%20Wizard%20F1%20Help.md)   
 [Dimensionstypen](../Topic/Dimension%20Types.md)  
  
  