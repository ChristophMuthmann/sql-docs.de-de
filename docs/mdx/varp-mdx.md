---
title: VarP (MDX) | Microsoft Docs
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
- VARP
dev_langs:
- kbMDX
helpviewer_keywords:
- VarP function [MDX]
ms.assetid: feca648d-bbc8-44c8-9a0e-38f66d914c72
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4f0d30afa0147f62bea4b58661ee735deb61a429
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="varp-mdx"></a>VarP (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Varianz eines numerischen Ausdrucks, ausgewertet über einer Menge mithilfe der unausgewogenen Auffüllungsformel (geteilt durch  *n* -1).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Die **VarP** Funktion gibt die unausgewogene Varianz eines angegebenen numerischen Ausdrucks, ausgewertet über einer angegebenen Menge zurück.  
  
 Die **VarP** -Funktion verwendet die unausgewogene Auffüllung Formel, während die [Var](../mdx/var-mdx.md) Funktion der Formel für die ausgewogene Auffüllung verwendet.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

