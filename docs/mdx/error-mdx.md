---
title: Fehler (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ERROR
dev_langs: kbMDX
helpviewer_keywords: Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 51be756a90d641032453370c214cbd37683a055c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="error-mdx"></a>Error (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
