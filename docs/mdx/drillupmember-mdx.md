---
title: DrillupMember (MDX) | Microsoft Docs
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
f1_keywords: DRILLUPMEMBER
dev_langs: kbMDX
helpviewer_keywords: DrillupMember function
ms.assetid: debcd966-ea4e-4ecf-8600-0a4d346d03f8
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9238f765f2dac6f892baffee15f473674fe5e8a7
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Elemente in einer angegebenen Menge zurück, die keine Nachfolger von Elementen in einer zweiten angegebenen Menge sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Set_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **DrillupMember** Funktion gibt eine Menge von Elementen basierend auf den in der ersten Menge angegebenen Elementen, die Nachfolger von Elementen in der zweiten Menge sind. Die erste Menge kann jede beliebige Dimensionalität aufweisen, die zweite muss jedoch eine eindimensionale Menge enthalten. Die Reihenfolge der Originalelemente in der ersten Menge wird beibehalten. Die Funktion erstellt die Menge, indem nur die Elemente aus der ersten Menge eingeschlossen werden, die unmittelbare nachfolgende Werte von Elementen in der zweiten Menge sind. Ist der unmittelbare Vorgänger eines Elements in der ersten Menge nicht in der zweiten vorhanden, wird das Element in der ersten Menge in die von der Funktion zurückgegebene Menge eingeschlossen. Nachfolgende Werte in der ersten Menge, die einem Vorgängerelement in der zweiten Menge vorausgehen, werden ebenfalls eingeschlossen.  
  
 Die erste Menge kann auch Tupel anstelle von Elementen enthalten. Der Drilldown für Tupel ist eine Erweiterung von OLE DB und gibt eine Menge von Tupeln anstelle von Elementen zurück.  
  
> [!IMPORTANT]  
>  Ein Drillup wird nur für ein Element durchgeführt, auf das direkt ein untergeordnetes Element oder ein Nachfolger folgt. Die Reihenfolge der Elemente in der Menge ist relevant für beide der Drilldown\* und Drillups\* Funktionsreihe. Erwägen Sie die **Hierarchize** Funktion, um die Elemente der ersten Menge entsprechend zu bestellen.  
  
## <a name="example"></a>Beispiel  
 Die folgenden drei Beispiele sind mit Ausnahme der zweiten Menge identisch. Im ersten Beispiel lautet der zweite Satz "Vereinigte Staaten". Demzufolge wird Colorado aus dem Resultset ausgeschlossen. Es ist ein untergeordnetes Element der Vereinigten Staaten.  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 Beispiel zwei zeigt die Wichtigkeit der Elementreihenfolge. Da **DrillupMember** Drillup nur auf den Elementen, deren Nachfolger in der ersten Menge unmittelbar folgen, er keinen Drillup auf dem Kanada-Element. Kanada wird vom Nachfolger durch die Vereinigten Staaten und Colorado getrennt. Wenn Sie die Elemente so neu anordnen, dass sich Kanada direkt über Alberta befindet, werden Alberta und Braunschweig aus dem Rowset ausgeschlossen.  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 Beispiel drei zeigt wie die Verwendung von **Hierarchize** können reduzieren die Auswirkungen der Elementreihenfolge, sodass ein Drillup auf dem Kanada-Element.  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
