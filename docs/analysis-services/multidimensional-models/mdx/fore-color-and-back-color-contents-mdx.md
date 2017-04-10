---
title: "FORE_COLOR- und BACK_COLOR-Inhalte (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FORE_COLOR-Inhalte"
  - "Hintergründe [MDX]"
  - "Zellen [MDX]"
  - "Farben [MDX]"
  - "Speichern von Zellenfarbeninformationen"
  - "Zellenhintergründe"
  - "BACK_COLOR-Inhalte"
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# FORE_COLOR- und BACK_COLOR-Inhalte (MDX)
  Die Zelleigenschaften **FORE_COLOR** und **BACK_COLOR** werden dazu verwendet, Farbinformationen für den Text bzw. den Hintergrund einer Zelle im RGB-Format (Rot-Grün-Blau) von Microsoft Windows zu speichern.  
  
 Der gültige Bereich für eine gewöhnliche RGB-Farbe ist 0 (null) bis 16.777.215 (&H00FFFFFF). Das höherwertige Byte einer Zahl in diesem Bereich entspricht immer 0. Die niederwertigen 3 Bytes bestimmen, vom niedrigsten zum höchsten Byte, den Anteil von Rot, Grün und Blau. Der rote, grüne und blaue Farbanteil werden jeweils durch eine Zahl zwischen 0 und 255 (&HFF) dargestellt.  
  
## Siehe auch  
 [Verwenden von Zelleneigenschaften &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-cell-properties-mdx.md)  
  
  