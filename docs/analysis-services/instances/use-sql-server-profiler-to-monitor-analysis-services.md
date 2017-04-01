---
title: "Verwenden von SQL Server Profiler zum &#220;berwachen von Analysis Services | Microsoft Docs"
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
  - "SQL Server Profiler, Analysis Services"
  - "Überwachen von Analysis Services [SQL Server]"
  - "Leistung [Analysis Services], SQL Server Profiler"
  - "Profiler [SQL Server Profiler], Analysis Services"
ms.assetid: 8b77dafc-4584-4e93-8ad7-299304391bfd
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# Verwenden von SQL Server Profiler zum &#220;berwachen von Analysis Services
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verfolgt Modulprozessereignisse wie das Starten eines Batches oder einer Transaktion und erfasst Daten zu diesen Ereignissen. So können Sie die Server- und Datenbankaktivität überwachen (z.B. Benutzerabfragen oder Anmeldeaktivität). Sie können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]-Daten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle oder -Datei aufzeichnen und später analysieren oder die aufgezeichneten Ereignisse in der gleichen oder einer anderen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz wiedergeben, um den genauen Ablauf anzuzeigen. Ereignisse können in Echtzeit oder schrittweise wiedergegeben werden. Sehr hilfreich ist es auch, die Ablaufverfolgungsereignisse zusammen mit den Leistungsindikatoren auf dem gleichen Computer auszuführen. Der Profiler kann diese auf der Grundlage von Zeit korrelieren und gemeinsam in einer einzelnen Zeitskala anzeigen. Ablaufverfolgungsereignisse bieten Ihnen mehr Details, während Leistungsindikatoren eine Aggregatsicht liefern. Informationen zum Erstellen und Ausführen von Ablaufverfolgungen finden Sie unter [Erstellen von Profilerablaufverfolgungen für Replay &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
 In der folgenden Tabelle werden die Themen in diesem Abschnitt beschrieben.  
  
## In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Einführung in die Überwachung von Analysis Services mit SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|Beschreibt das Verwenden von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zum Überwachen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz.|  
|[Erstellen von Profilerablaufverfolgungen für Replay &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)|Beschreibt die Anforderungen für das Erstellen einer Ablaufverfolgung zur Wiedergabe mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md)|Beschreibt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Ereignisklassen. Diese Ereignisklassen sind Aktionen zugeordnet, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generiert werden, und werden zum Wiedergeben von Ablaufverfolgungen verwendet.|  
  
## Siehe auch  
 [Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  