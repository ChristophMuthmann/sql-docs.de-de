---
title: Fehlerbehandlung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1eb0133bb4f6e1d4b03e83f771c6170204eeb5b8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="error-handling-mdx"></a>Fehlerbehandlung (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Jeder Cube kann steuern, wie Fehler in einem Skript MDX (Multidimensional Expressions) behandelt werden. Die Fehlerbehandlung erfolgt über den **ScriptErrorHandlingMode** -Enumerator. Für diesen Enumerator sind folgende Werte möglich:  
  
 **IgnoreNone**  
 Veranlasst den Server, einen Fehler auszulösen, wenn [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] einen Fehler im MDX-Skript gefunden hat.  
  
 **IgnoreAll**  
 Veranlasst den Server dazu, alle Befehle im MDX-Skript zu ignorieren, die einen Fehler (Syntaxfehler, Fehler bei der Namensauflösung usw.) enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
