---
title: + (Vereinigung) (MDX) | Microsoft Docs
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
- +
dev_langs:
- kbMDX
helpviewer_keywords:
- union operator (+)
- + (union operator)
ms.assetid: 6c6dfca2-7413-452a-98a2-3d8c58a8a3e6
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 49da0620fba34bf198a5d343ef7a8c5350c1cea8
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="union---mdx-operator-reference"></a>Union - MDX-operatorreferenz
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt eine Mengenoperation aus, die die Vereinigungsmenge zweier Mengen zurückgibt. Dabei werden doppelte Elemente entfernt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>Parameter  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Eine Menge, die die Elemente der beiden angegebenen Mengen enthält.  
  
## <a name="remarks"></a>Hinweise  
 Die **+ (Union)** Operator ist funktionell gleichwertig mit der [Union &#40; MDX &#41; ](../mdx/union-mdx.md) Funktion.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung dieses Operators.  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

