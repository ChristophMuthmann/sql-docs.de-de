---
title: AllMembers (MDX) | Microsoft Docs
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
f1_keywords: ALLMEMBERS
dev_langs: kbMDX
helpviewer_keywords: AllMembers function
ms.assetid: 202e81d4-d2ee-4ec1-a019-4835eb19f446
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b4953bd5bff4ab578cc492991918ee5c90abb7a1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Wertet entweder einen Hierarchie- oder einen Ebenenausdruck aus und gibt eine Menge zurück, die alle Elemente der angegebenen Hierarchie oder Ebene enthält. Hierzu zählen alle berechneten Elemente der Hierarchie oder Ebene.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>Argumente  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **AllMembers** -Funktion eine Menge, die alle Elemente enthält, einschließlich berechneter Elemente in der angegebenen Hierarchie oder Ebene zurück. Die **AllMembers** Funktion gibt die berechneten Elemente zurück, selbst wenn die angegebene Hierarchie oder Ebene keine sichtbaren Elemente enthält.  
  
> [!IMPORTANT]  
>  Wenn eine Dimension nur eine einzige sichtbare Hierarchie enthält, kann auf die Hierarchie entweder mit dem Dimensionsnamen oder mit dem Hierarchienamen verwiesen werden, weil der Dimensionsname in diesem Fall in seine einzige sichtbare Hierarchie aufgelöst wird. `Measures.AllMembers` ist z. B. ein gültiger MDX-Ausdruck, weil er in die einzige vorhandene Hierarchie in der Measures-Dimension aufgelöst wird.  
  
> [!NOTE]  
>  Die **AllMembers** -Funktion ähnelt semantisch der [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) Funktion.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt alle Elemente in der [`Date].[Calendar Year]` Attributhierarchie auf der Spaltenachse, dies schließt berechnete Elemente und die Menge aller untergeordneten Elemente von der `[Product].[Model Name]` -Attributhierarchie auf der Zeilenachse der **Adventure Works** Cube.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 Das folgende Beispiel gibt alle Elemente in der **Measures** Dimension auf der Spaltenachse einschließlich aller berechneten Elemente sowie die Menge aller untergeordneten Elemente der der `[Product].[Model Name]` -Attributhierarchie auf der Zeilenachse der **Adventure Works** Cube.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [AddCalculatedMembers &#40; MDX &#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Untergeordnete Elemente &#40; MDX &#41;](../mdx/children-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
