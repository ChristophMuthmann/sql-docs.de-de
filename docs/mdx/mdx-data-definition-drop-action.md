---
title: DROP ACTION-Anweisung (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dd8e7776899331a089fb12157a072e4ade673655
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-action"></a>MDX-Datendefinition - DROP-Aktion
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Löscht eine angegebene Aktion aus einem angegebenen Cube.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Cubenamen bereitstellt.  
  
 *Aktionsname*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen der zu löschenden Aktion bereitstellt.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE ACTION-Anweisung &#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)   
 [MDX-Datendefinitionsanweisungen &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
