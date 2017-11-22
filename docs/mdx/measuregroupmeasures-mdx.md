---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: baacb5ee83ecd45bc994cc462b04d35d6d3ca15a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Menge der Measures zurück, die zur angegebenen Measuregruppe gehören.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumente  
 *MeasureGroupName*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen der Measuregruppe enthält, aus der die Menge der Measures abgerufen werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Die angegebene Zeichenfolge muss genau mit dem Namen der Measuregruppe übereinstimmen. Die Verwendung von eckigen Klammern für Measuregruppennamen, die Leerzeichen enthalten, ist nicht erforderlich.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden alle Measures in der Internet Sales-Measuregruppe im Adventure Works-Cube zurückgegeben.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
