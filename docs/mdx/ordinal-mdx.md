---
title: Ordinalzahl (MDX) | Microsoft Docs
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
f1_keywords: Ordinal
dev_langs: kbMDX
helpviewer_keywords: Ordinal function
ms.assetid: 9d416c39-da4a-4f0d-8d85-a76af5df0a87
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2cf441cb5eaaba8ec7b0e14adb1f770464006abb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den nullbasierten Ordinalwert, der einer Ebene zugeordnet ist, zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argumente  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Ordinal** -Funktion wird häufig in Verbindung mit der **IIF** und **CurrentMember** Funktionen, um unterschiedliche Werte bedingt auf verschiedenen Hierarchieebenen anzuzeigen auf Grundlage der Position der einzelnen speziellen Zellen im Abfrageergebnis vorhergesagt. Beispielsweise können Sie die **Ordnungszahl** -Funktion Berechnungen auf bestimmten Ebenen ausführen und den Standardwert "N/v" auf anderen Ebenen angezeigt.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Ordinalzahl für die Calendar Quarter-Ebene in der Calendar-Hierarchie zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
