---
title: Diese (MDX) | Microsoft Docs
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
- THIS
dev_langs:
- kbMDX
helpviewer_keywords:
- This function [MDX]
ms.assetid: 87acddee-ae54-49ee-8923-1b760606e8b7
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 87d902437558a4637d4f67c8338d40c3c3a361b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="this-mdx"></a>This (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den aktuellen Teilcube zum Verwenden mit Zuweisungen im MDX-Berechnungsskript (Multidimensional Expressions) zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
This   
```  
  
## <a name="remarks"></a>Hinweise  
 Die **dies** Funktion Teilcubeausdrucks verwendet werden kann, um den aktuellen Teilcube im aktuellen Gültigkeitsbereich innerhalb des MDX-Berechnungsskripts bereitzustellen. Die **dies** Funktion muss auf der linken Seite einer Zuweisung verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Fragment eines MDX-Scripts veranschaulicht die Verwendung des This-Schlüsselworts mit SCOPE-Anweisungen, um Zuweisungen an Teilcubes vorzunehmen:  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2005],`  
  
 `[Date].[Fiscal].[Fiscal Quarter].Members,`  
  
 `[Measures].[Sales Amount Quota]`  
  
 `) ;`  
  
 `This = ParallelPeriod`  
  
 `(`  
  
 `[Date].[Fiscal].[Fiscal Year], 1,`  
  
 `[Date].[Fiscal].CurrentMember`  
  
 `) * 1.35 ;`  
  
 `/*-- Allocate equally to months in FY 2002 -----------------------------*/`  
  
 `Scope`  
  
 `(`  
  
 `[Date].[Fiscal Year].&[2002],`  
  
 `[Date].[Fiscal].[Month].Members`  
  
 `) ;`  
  
 `This = [Date].[Fiscal].CurrentMember.Parent / 3 ;`  
  
 `End Scope ;`  
  
 `End Scope;`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)   
 [Berechnungen](../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
