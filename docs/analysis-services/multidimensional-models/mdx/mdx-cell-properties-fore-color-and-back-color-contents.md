---
title: FORE_COLOR- und BACK_COLOR-Inhalte (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 921f3bb6b8d8458d534ecd629aa6eba52fe704ae
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>MDX-Cell Properties - FORE_COLOR- und BACK_COLOR-Inhalte
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Die **FORE_COLOR** und **BACK_COLOR** Zelleigenschaften Farbinformationen für den Text und Hintergrund einer Zelle, in der Microsoft Windows Betriebssystem Rot-Grün-Blau (RGB)-Format speichern .  
  
 Der gültige Bereich für eine gewöhnliche RGB-Farbe ist 0 (null) bis 16.777.215 (&H00FFFFFF). Das höherwertige Byte einer Zahl in diesem Bereich entspricht immer 0. Die niederwertigen 3 Bytes bestimmen, vom niedrigsten zum höchsten Byte, den Anteil von Rot, Grün und Blau. Der rote, grüne und blaue Farbanteil werden jeweils durch eine Zahl zwischen 0 und 255 (&HFF) dargestellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Zelleneigenschaften &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
