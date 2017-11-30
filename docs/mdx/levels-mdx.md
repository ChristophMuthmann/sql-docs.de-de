---
title: Ebenen (MDX) | Microsoft Docs
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
f1_keywords: Levels
dev_langs: kbMDX
helpviewer_keywords: Levels function
ms.assetid: 1a989cc9-8aa8-4ec3-b5e9-795d6fa84983
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 430577931bf30260a190e6541aa94ddc12b70435
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="levels-mdx"></a>Levels (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Ebene zurück, deren Position in einer Dimension oder Hierarchie durch einen numerischen Ausdruck angegeben ist oder deren Name durch einen Zeichenfolgenausdruck angegeben ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>Argumente  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
 *Level_Number*  
 Ein gültiger numerischer Ausdruck, der eine Ebenennummer angibt.  
  
 *Ebenenname*  
 Ein gültiger Zeichenfolgenausdruck, der einen Ebenennamen angibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Ebenennummer angegeben wird, die **Ebenen** zurückgegeben, die auf der angegebenen nullbasierten Position zugeordnet.  
  
 Wenn ein Ebenenname angegeben wird, die **Ebenen** Funktion die angegebene Ebene zurück.  
  
> [!NOTE]  
>  Verwenden Sie die Syntaxvariante mit dem Zeichenfolgenausdruck für benutzerdefinierte Funktionen.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen aller der **Ebenen** Syntaxen-Funktion.  
  
### <a name="numeric"></a>Numerisch  
 Im folgenden Beispiel wird die Country-Ebene zurückgegeben:  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 Im folgenden Beispiel wird die Country-Ebene zurückgegeben:  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
