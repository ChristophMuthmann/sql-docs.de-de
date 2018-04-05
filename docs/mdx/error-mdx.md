---
title: Fehler (MDX) | Microsoft Docs
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
- ERROR
dev_langs:
- kbMDX
helpviewer_keywords:
- Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5b17e524eaf357988b3fb7c4ee46a0ba25e6df18
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="error-mdx"></a>Error (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Löst einen Fehler aus. Optional wird eine angegebene Fehlermeldung ausgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Fehlertext*  
 Ein gültiger Zeichenfolgenausdruck, der die zurückzugebende Fehlermeldung enthält.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage zeigt, wie die **Fehler** Funktion in einem berechneten Measure:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
