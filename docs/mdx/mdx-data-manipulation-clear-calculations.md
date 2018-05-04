---
title: CLEAR CALCULATIONS-Anweisung (MDX) | Microsoft Docs
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
- CLEAR CALCULATIONS
- clalculations
- clear
dev_langs:
- kbMDX
helpviewer_keywords:
- clearing calculations
- CLEAR CALCULATIONS statement
- deleting calculations
- removing calculations
- calculations [Analysis Services], clearing
- cubes [Analysis Services], calculations
ms.assetid: aebec9a1-1d1d-4697-aa3f-cc2449625603
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 84cfc46ea64b0d4fb1dd79532bc6bdba9af71ded
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Datenbearbeitung für MDX - CLEAR CALCULATIONS
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Entfernt alle Berechnungen aus dem Cube und setzt den Cube auf den Berechnungsdurchlauf 0 zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Expression*  
 Ein gültiger MDX-Cubeausdruck (Multidimensional Expressions).  
  
## <a name="remarks"></a>Hinweise  
 Die **FROM** -Klausel kann ausgelassen werden, wenn der Kontext des Cubes bekannt, z. B. in einem MDX-Skript ist.  
  
> [!NOTE]  
>  Diese Anweisung kann nur von einem Server- oder Datenbankadministrator oder einem Mitglied einer Rolle mit Zugriff auf die Quelldaten des Cubes (das heißt ReadSourceData=true) ausgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datenbearbeitungsanweisungen &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
