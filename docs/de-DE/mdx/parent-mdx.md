---
title: Parent (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PARENT
dev_langs:
- kbMDX
helpviewer_keywords:
- Parent function
ms.assetid: 7be9b172-4241-4618-bdba-53cde8badd9b
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 62586e6e5f7246777079f2e68b3d8a0a92041178
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="parent-mdx"></a>Parent (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das übergeordnete Element eines Elements zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **übergeordneten** Funktion gibt das übergeordnete Element des angegebenen Elements zurück.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen wird das übergeordnete Element des July 1, 2001-Elements zurückgegeben. Im ersten Beispiel ist dieses Element im Kontext der Date-Attributhierarchie angegeben. Zurückgegeben wird das All Periods-Element.  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel ist das July 1, 2001-Element im Kontext der Calendar-Hierarchie angegeben.  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
