---
title: "Definieren von Faktenbeziehungen und Faktenbeziehungseigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
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
  - "Faktendimensionen [Analysis Services]"
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Definieren von Faktenbeziehungen und Faktenbeziehungseigenschaften
  Wenn Sie eine neue Cubedimension oder eine neue Measuregruppe definieren, versucht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], zu erkennen, ob eine Faktendimensionsbeziehung vorhanden ist, und legt dann die Einstellung für die Dimensionsverwendung auf **Fakt** fest. Sie können eine Faktendimensionsbeziehung im Cube-Designer auf der Registerkarte **Dimensionsverwendung** anzeigen oder bearbeiten. Die Faktenbeziehung zwischen einer Dimension und einer Measuregruppe besitzt die folgenden Einschränkungen:  
  
-   Eine Cubedimension kann nur über eine Faktenbeziehung zu einer bestimmten Measuregruppe verfügen.  
  
-   Eine Cubedimension kann über separate Faktenbeziehungen zu mehreren Measuregruppen verfügen.  
  
-   Beim Granularitätsattribut der Beziehung muss es sich um das Schlüsselattribut (z. B. Transaction Number) für die Dimension handeln. Hierdurch wird eine 1:1-Beziehung zwischen der Dimension und den Fakten in der Faktentabelle erstellt.  
  
  