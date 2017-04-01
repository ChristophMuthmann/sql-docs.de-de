---
title: "Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Korrelieren von Ablaufverfolgungen mit Protokolldaten"
  - "Protokolle [SQL Server], Ablaufverfolgungen"
  - "Profiler [SQL Server Profiler] Korrelieren der Ablaufverfolgung mit Protokolldaten"
  - "Ablaufverfolgungen [SQL Server], Protokolle"
  - "SQL Server Profiler, Korrelieren der Ablaufverfolgung mit Protokolldaten"
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten
  Mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]können Sie ein Microsoft Windows-Leistungsprotokoll öffnen, die Leistungsindikatoren auswählen, die Sie mit einer Ablaufverfolgung korrelieren möchten, und die ausgewählten Leistungsindikatoren zusammen mit der Ablaufverfolgung auf der grafischen Benutzeroberfläche von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] anzeigen. Wenn Sie ein Ereignis im Ablaufverfolgungsfenster auswählen, zeigt ein senkrechter roter Strich im Datenfensterbereich des Systemmonitors von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] an, welche Leistungsprotokolldaten mit dem ausgewählten Ablaufverfolgungsereignis korrelieren.  
  
 Um eine Ablaufverfolgung mit Leistungsindikatoren zu korrelieren, öffnen Sie eine Ablaufverfolgungsdatei oder -tabelle, die die Datenspalten **StartTime** und **EndTime** data columns, und then click **Datei** von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Leistungsdaten importieren** . Anschließend können Sie das Leistungsprotokoll öffnen und die Systemmonitor-Objekte und -Leistungsindikatoren auswählen, die Sie mit der Ablaufverfolgung korrelieren möchten.  
  
## Siehe auch  
 [Korrelieren einer Ablaufverfolgung mit Windows-Leistungsprotokolldaten &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  