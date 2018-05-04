---
title: HIERARCHIZE (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HIERARCHIZE
dev_langs:
- kbMDX
helpviewer_keywords:
- Hierarchize function
ms.assetid: e9795003-70e7-4b4c-9074-45b5b9b817fa
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: f878ccfcba9c23d6ace65dd101beef202832bb9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ordnet die Elemente einer Menge hierarchisch an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Hierarchize** -Funktion ordnet die Elemente der angegebenen Menge in hierarchischer Reihenfolge. Die Funktion behält Duplikate immer bei.  
  
-   Wenn **POST** nicht angegeben wird, sortiert die Funktion die Elemente in einer Ebene in ihrer natürlichen Reihenfolge. Die natürliche Reihenfolge stellt die Standardsortierung der Elemente in der Hierarchie dar, wenn keine anderen Sortierbedingungen angegeben werden. Untergeordnete Elemente werden unmittelbar nach ihren übergeordneten Elementen angeordnet.  
  
-   Wenn **POST** angegeben wird, die **Hierarchize** -Funktion sortiert die Elemente einer Ebene in der Postorder-Reihenfolge. Untergeordnete Elemente gehen also den ihnen übergeordneten Elementen voran.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein Drillup für das Canada-Element durchgeführt. Die **Hierarchize** Funktion wird verwendet, um die angegebenen Elemente der Menge in hierarchischer Reihenfolge organisieren erforderlich die **DrillUpMember** Funktion.  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 Das folgende Beispiel gibt die Summe der `Measures.[Order Quantity]` Elements, aggregiert über die ersten neun Monate von 2003 in der `Date` Dimension, aus der **Adventure Works** Cube. Die **PeriodsToDate** -Funktion definiert die Tupel in der Menge, die über die die Aggregatfunktion angewendet wird. Die **Hierarchize** -Funktion ordnet die Elemente der angegebenen Menge von Elementen aus der Product-Dimension in hierarchischer Reihenfolge.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
