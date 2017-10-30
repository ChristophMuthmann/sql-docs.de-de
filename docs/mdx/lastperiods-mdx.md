---
title: LastPeriods (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LASTPERIODS
dev_langs:
- kbMDX
helpviewer_keywords:
- LastPeriods function
ms.assetid: a15df7a1-b261-48ed-aacc-d2804db8dbf7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dc24f14f734c697946226974a8d51761a6d8182e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Menge von Elementen bis zu einem angegebenen Element, einschließlich des Elements, zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Index*  
 Ein gültiger numerischer Ausdruck, der eine Anzahl von Zeiträumen angibt.  
  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die angegebene Anzahl von Zeiträumen positiv ist, wird die **LastPeriods** Funktion gibt eine Menge von Elementen, die mit dem Element beginnen, die zurückliegen *Index* -1 aus dem angegebenen Elementausdruck befindet und endet mit dem angegebenen Element. Die Anzahl der von der Funktion zurückgegebenen Elemente entspricht *Index*.  
  
 Wenn die angegebene Anzahl von Zeiträumen negativ ist, wird die **LastPeriods** Funktion gibt eine Menge von Elementen, die mit dem angegebenen Element beginnt und endet mit dem Element, das führt (- *Index* - 1) aus den angegebenen Member auf. Die Anzahl der von der Funktion zurückgegebenen Elemente gleich den absoluten Wert des *Index*.  
  
 Wenn die angegebene Anzahl von Zeiträumen NULL ist, ist die **LastPeriods** Funktion die leere Menge zurück. Dies ist im Gegensatz zu den **Lag** -Funktion, die das angegebene Element zurück, wenn 0 angegeben wird.  
  
 Wenn ein Element nicht angegeben wird, die **LastPeriods** Funktion verwendet **Time.CurrentMember**. Wenn keine Dimension als Time-Dimension markiert ist, wird die Funktion fehlerfrei analysiert und ausgeführt, erzeugt aber bei der Clientanwendung einen Zellenfehler.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Standardmeasurewert für das zweite, dritte und vierte Geschäftsquartal des Geschäftsjahres 2002 zurückgegeben.  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Diese Beispiel kann auch mithilfe des Doppelpunkt-Operators (:) formuliert werden:  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 Im folgenden Beispiel wird der Standardmeasurewert für das erste Quartal im Geschäftsjahr 2002 zurückgegeben. Obwohl für die Anzahl der Zeiträume 3 angegeben wurde, kann nur der Wert für einen Zeitraum zurückgegeben werden, da es keine Zeiträume gibt, die vor dem angegebenen im Geschäftsjahr liegen.  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

