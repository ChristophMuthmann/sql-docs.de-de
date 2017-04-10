---
title: "Definieren von Attributbeziehungen | Microsoft Docs"
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
  - "Attribute [Analysis Services], Beziehungen"
  - "Beziehungen [Analysis Services], Attribute"
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Definieren von Attributbeziehungen
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]sind Attribute der grundlegende Baustein einer Dimension. Eine Dimension enthält einen Satz von Attributen, die auf Basis von Attributbeziehungen organisiert sind.  
  
 Für jede Tabelle in einer Dimension existiert eine Attributbeziehung, die das Schlüsselattribut der Tabelle mit anderen Attributen aus der Tabelle verknüpft. Diese Beziehung kommt zustande, wenn Sie die Dimension erstellen.  
  
 Eine Attributbeziehung bietet die folgenden Vorteile:  
  
-   Sie reduziert den für die Dimensionsverarbeitung erforderlichen Speicherplatz. Dies beschleunigt die Dimensions-, Partitions- und Abfrageverarbeitung.  
  
-   Sie erhöht die Abfrageleistung, da der Speicherzugriff beschleunigt wird und Ausführungspläne besser optimiert werden können.  
  
-   Sie führt aufgrund der Aggregationsentwurfsalgorithmen zur Auswahl effektiverer Aggregate, sofern benutzerdefinierte Hierarchien entlang den Beziehungspfaden definiert wurden.  
  
    > [!NOTE]  
    >  Weitere Informationen über die Bedeutung und die Auswirkungen der Definition und Konfiguration von Attributbeziehungen finden Sie im Abschnitt „Enhancing query performance“ (Verbessern der Abfrageleistung) im [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## Überlegungen zu Attributbeziehungen  
 Sofern die zugrunde liegenden Daten dies unterstützen, sollten Sie auch eindeutige Attributbeziehungen zwischen Attributen definieren. Um eindeutige Attributbeziehungen zu definieren, verwenden Sie die Registerkarte **Attributbeziehungen** des Dimensions-Designers.  
  
 Jedes Attribut, das über eine ausgehende Beziehung verfügt, muss über einen eindeutigen Schlüssel relativ zu seinem verknüpften Attribut verfügen. Anders ausgedrückt darf ein Element in einem Quellattribut nur ein Element in einem verknüpften Attribut identifizieren. Betrachten Sie z. B. die Beziehung "City -> State". In dieser Beziehung ist "City" das Quellattribut und "State" das verknüpfte Attribut. Das Quellattribut entspricht der Seite "m" und die verknüpfte Seite entspricht der Seite "1" der m:1-Beziehung. Der Schlüssel für das Quellattribut lautet "City + Status". Weitere Informationen finden Sie unter [Gewusst wie: Erstellen, Ändern oder Löschen einer Attributbeziehung](../../analysis-services/multidimensional-models/create-modify-or-delete-an-attribute-relationship.md).  
  
 Weitere Informationen zu Eigenschaften einer Attributbeziehung finden Sie unter [Konfigurieren von Attributbeziehungseigenschaften](../../analysis-services/multidimensional-models/configure-attribute-relationship-properties.md).  
  
> [!NOTE]  
>  Eine falsche Definition von Attributbeziehungen kann zu ungültigen Abfrageergebnissen führen.  
  
## Siehe auch  
 [Attributbeziehungen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  