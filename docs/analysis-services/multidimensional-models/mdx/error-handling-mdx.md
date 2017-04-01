---
title: "Fehlerbehandlung (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "Skripts [MDX], Ausnahmen"
  - "Ausnahmen [MDX]"
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# Fehlerbehandlung (MDX)
  Jeder Cube kann steuern, wie Fehler in einem MDX-Skript (Multidimensional Expressions) behandelt werden. Die Fehlerbehandlung erfolgt über den **ScriptErrorHandlingMode** -Enumerator. Für diesen Enumerator sind folgende Werte möglich:  
  
 **IgnoreNone**  
 Veranlasst den Server, einen Fehler auszulösen, wenn [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] einen Fehler im MDX-Skript gefunden hat.  
  
 **IgnoreAll**  
 Veranlasst den Server dazu, alle Befehle im MDX-Skript zu ignorieren, die einen Fehler (Syntaxfehler, Fehler bei der Namensauflösung usw.) enthalten.  
  
## Siehe auch  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  