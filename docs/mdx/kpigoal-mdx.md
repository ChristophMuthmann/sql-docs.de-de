---
title: KPIGoal-Element (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: KPIGoal function
ms.assetid: 0122c7d5-eefc-4819-b7a9-c80cd35505a8
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bdd010f81a1454e9714c76352754f33ac6951952
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="kpigoal-mdx"></a>KPIGoal (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das Element zurück, das den Wert für den Zielanteil des angegebenen Key Performance Indicators (KPI) berechnet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
KPIGoal(KPI_Name)  
```  
  
## <a name="arguments"></a>Argumente  
 *KPI_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen eines KPIs angibt.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel gibt die KPI-Wert des KPI-Ziels, KPI-Status und KPI-Trend für das Channel Revenue-Measure für die nachfolgenden Werte dreier Elemente der Fiscal Year-Attributhierarchie zurück:  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
