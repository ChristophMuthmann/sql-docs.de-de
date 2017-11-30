---
title: IF-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: statements [MDX], IF
ms.assetid: 8830cce5-9e06-4f89-a555-295bb0d0a8a1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3bfc3eb927d6e9764349281ea48ef94e7873675b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-scripting---if"></a>MDX-Skripts - IF
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine Anweisung aus, wenn die Bedingung erfüllt ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein MDX-Ausdruck (Multidimensional Expressions), der zu einem booleschen Wert ausgewertet wird, der TRUE oder FALSE zurückgibt.  
  
 *Zuweisung*  
 Ein MDX-Ausdruck, der entweder einem Teilcube oder einer berechneten Eigenschaft einen Wert zuweist.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie die IF-Anweisung für die ablaufsteuerung, also im Gegensatz zu den [IIf &#40; MDX &#41; ](../mdx/iif-mdx.md) Funktion und die [CASE-Anweisung &#40; MDX &#41; ](../mdx/case-statement-mdx.md) , nur zum Zurückgeben von Werten oder Objekten verwendet werden kann.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel ist der Gültigkeitsbereich auf die Country-Ebene der Customer Geography-Hierarchie in der Customer-Dimension beschränkt. Wenn das aktuelle Measure „Betrag der Internetsteuern“ ist, dann wird „Betrag der Internetsteuern“ auf 10 festgelegt:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
