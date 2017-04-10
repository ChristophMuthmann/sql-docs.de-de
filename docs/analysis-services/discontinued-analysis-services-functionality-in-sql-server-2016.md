---
title: "Nicht mehr unterst&#252;tzte Analysis Services-Funktionalit&#228;t in SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, backward compatibility"
  - "SSAS, Abwärtskompatibilität"
  - "SQL Server Analysis Services, Abwärtskompatibilität"
  - "Nicht mehr unterstützte Funktionalität [Analysis Services]"
  - "Nicht unterstützte Funktionen [Analysis Services]"
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
caps.latest.revision: 43
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 43
---
# Nicht mehr unterst&#252;tzte Analysis Services-Funktionalit&#228;t in SQL Server 2016
  Eine *nicht mehr unterstützte Funktion* ist eine veraltete Funktion, die nicht länger unterstützt wird. Eventuell wurde sie sogar aus dem Produkt entfernt. Die folgenden Funktionen werden ab [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] nicht mehr unterstützt.  
  
|||  
|-|-|  
|**Funktion**|**Alternative oder Problemumgehung**|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Keine. Diese Funktion wurde in SQL Server 2005 als veraltet markiert.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|Keine. Diese Funktion wurde in SQL Server 2005 als veraltet markiert.|  
|Hinweis NON_EMPTY_BEHAVIOR für den Abfrageoptimierer|Keine. Diese Funktion wurde in SQL Server 2008 als veraltet markiert.|  
|COM-Assemblys|Keine. Diese Funktion wurde in SQL Server 2008 als veraltet markiert.|  
|Systeminterne Zelleneigenschaft CELL_EVALUATION_LIST|Keine. Diese Funktion wurde in SQL Server 2005 als veraltet markiert.|  
  
> [!NOTE]  
>  Zuvor als veraltet markierte Ankündigungen von Funktionen aus [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] bleiben wirksam. Da der Code, der diese Funktionen unterstützt, noch nicht aus dem Produkt-entfernt wurde, sind viele dieser Funktionen in dieser Version weiterhin vorhanden. Obwohl auf zuvor als veraltet markierte Funktionen möglicherweise zugegriffen werden kann, gelten sie noch immer als veraltet und könnten zu jedem beliebigen Zeitpunkt zwischen der Veröffentlichung der [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Version und der Nachfolgeversion physisch aus dem Produkt gelöscht werden. Es wird dringend empfohlen, dass Sie keine als veraltet markierten Funktionen in neuen Modellen oder Anwendungen basierend auf [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] verwenden.  
  
## Siehe auch  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)   
 [Veraltete Analysis Services-Funktionen in SQL Server 2016](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md)  
  
  