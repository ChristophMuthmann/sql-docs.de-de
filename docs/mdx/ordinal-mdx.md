---
title: Ordinalzahl (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Ordinal
dev_langs:
- kbMDX
helpviewer_keywords:
- Ordinal function
ms.assetid: 9d416c39-da4a-4f0d-8d85-a76af5df0a87
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b848698799bc0c620d9592e90f508f01ac279f6f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  

