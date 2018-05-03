---
title: LinkMember (MDX) | Microsoft Docs
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
- LINKMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 3201ea45c940c4d08956192203a167436c4135f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das Element zurück, das in einer angegebenen Hierarchie gleichbedeutend mit dem angegebenen Element ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **LinkMember** Funktion gibt das Element zurück, aus der angegebenen Hierarchie, die die Schlüsselwerte auf jeder Ebene des angegebenen Elements in einer zugehörigen Hierarchie entspricht. Die Attribute auf jeder Ebene müssen die gleiche Schlüsselkardinalität und den gleichen Datentyp aufweisen. Wenn es bei unnatürlichen Hierarchien mehr als eine Entsprechung für den Schlüsselwert eines Attributs gibt, ist das Resultat ein Fehler oder unbestimmt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die **LinkMember** Funktion, um das Standardmeasure im Adventure Works-Cube für die Vorgänger des July 1, 2002-Elements der Date.Date-Attributhierarchie in der Calendar-Hierarchie zurückzugeben.  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [HIERARCHIZE & #40; MDX & #41;](../mdx/hierarchize-mdx.md)   
 [ASCENDANTS &#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
