---
title: Eigenschaften (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Properties
dev_langs: kbMDX
helpviewer_keywords: Properties function
ms.assetid: 2d8442c5-30c4-4fd1-99ea-9845b6533e41
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1931694b7054dec03c45617867ccf4a68575fd09
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="properties-mdx"></a>Properties (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Zeichenfolge oder einen stark typisierten Wert zurück, der den Wert einer Elementeigenschaft enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Eigenschaftsname*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen einer Elementeigenschaft enthält.  
  
## <a name="remarks"></a>Hinweise  
 Die **Eigenschaften** Funktion gibt den Wert des angegebenen Elements für die angegebene Elementeigenschaft zurück. Die Member-Eigenschaft werden alle systeminternen Elementeigenschaften, wie z. B. **Namen**, **ID**, **Schlüssel**, oder **Beschriftung**, oder es kann eine benutzerdefinierte Elementeigenschaft sein. Weitere Informationen finden Sie unter [systeminterne Elementeigenschaften &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) und [benutzerdefinierte Elementeigenschaften &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 Standardmäßig muss der Wert zwingend eine Zeichenfolge sein. Wenn **TYPISIERTEN** angegeben ist, wird der Rückgabewert stark typisiert ist.  
  
-   Bei einer systeminternen Eigenschaft gibt die Funktion den ursprünglichen Typ des Elements zurück.  
  
-   Der Eigenschaftentyp eine benutzerdefinierte, der Typ des Rückgabewerts ist identisch mit dem Typ des Rückgabewerts der der **MemberValue** Funktion.  
  
> [!NOTE]  
>  Properties ('Key') gibt das gleiche Ergebnis wie Key0 zurück, außer für zusammengesetzte Schlüssel. Properties ('Key') gibt für zusammengesetzte Schlüssel den Wert NULL zurück. Verwenden Sie die Taste*x* Syntax für zusammengesetzte Schlüssel, wie im Beispiel veranschaulicht. Properties ('Key0'), Properties('Key1'), Properties('Key2') usw. bilden zusammen den zusammengesetzten Schlüssel.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden sowohl systemeigene als auch benutzerdefinierte Elementeigenschaften zurückgegeben. Dabei wird das TYPED-Argument verwendet, um den stark typisierten Wert für die Day Name-Elementeigenschaft zurückzugeben.  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 Das folgende Beispiel zeigt die Verwendung des Schlüssels*x* Eigenschaft.  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Elementeigenschaften &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
