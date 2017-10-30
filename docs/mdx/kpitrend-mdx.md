---
title: KPITrend (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- KPITrend function
ms.assetid: 0afd4513-af6e-4517-8e69-177bc7807d03
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 01476374e7fdb320a500a2e6afcdf28cbf27627b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="kpitrend-mdx"></a>KPITrend (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den normalisierten Wert zurück, der den Trendanteil des Key Performance Indicators (KPI) darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
KPITrend(KPI_Name)  
```  
  
## <a name="arguments"></a>Argumente  
 *KPI_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen des KPIs angibt.  
  
## <a name="remarks"></a>Hinweise  
 Der Trendwert ist im Allgemeinen ein normalisierter Wert zwischen -1 und 1.  
  
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
  
  

