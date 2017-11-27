---
title: Verwenden von Elementfunktionen | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- member functions [MDX]
ms.assetid: 094c443f-0daa-4af7-801c-d2e1d686d755
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9354c2e6a83918742f1c2de1dea943be4b21e844
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="using-member-functions"></a>Verwenden von Elementfunktionen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Eine Elementfunktion ist eine Multidimensional Expressions (MDX)-Funktion, die ein Element zurückgibt. Elementfunktionen sind genau wie Tupelfunktionen und Mengenfunktionen wesentlich für das Aushandeln mehrdimensionaler Strukturen, die in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zu finden sind.  
  
 Von den zahlreichen Elementfunktionen in MDX am wichtigsten ist die **CurrentMember** -Funktion, die verwendet wird, um das aktuelle Element in einer Hierarchie zu ermitteln. Die folgende Abfrage zeigt, wie sie zusammen mit der **übergeordneten**, **Vorgänger**, und **Prevmember** Funktionen:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; MDX-Syntax &#41;](../mdx/functions-mdx-syntax.md)   
 [Verwenden von Tupelfunktionen](../mdx/using-tuple-functions.md)   
 [Verwenden von Mengenfunktionen](../mdx/using-set-functions.md)  
  
  

