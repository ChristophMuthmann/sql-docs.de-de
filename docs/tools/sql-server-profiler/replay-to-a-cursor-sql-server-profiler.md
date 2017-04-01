---
title: "Wiedergeben bis zu einer Cursorposition (SQL Server Profiler) | Microsoft Docs"
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
  - "Wiedergeben von Cursors"
  - "Ablaufverfolgungen [SQL Server], wiedergeben"
  - "Wiedergeben von Ablaufverfolgungen"
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# Wiedergeben bis zu einer Cursorposition (SQL Server Profiler)
  In diesem Thema wird beschrieben, wie Ablaufverfolgungsdateien oder -tabellen mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]so wiedergegeben werden können, dass sie anhalten, wenn sie eine Cursorposition erreichen. Durch das Anhalten von Ablaufverfolgungen an Cursorpositionen wird das Debugging erleichtert, da lange Ablaufverfolgungsskripts in kürzere Segmente unterteilt und inkrementell analysiert werden können.  
  
### So geben Sie bis zur Cursorposition wieder  
  
1.  Öffnen Sie die Ablaufverfolgungsdatei oder -tabelle, die Sie wiedergeben möchten. Weitere Informationen finden Sie unter [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) oder unter [Öffnen einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Stellen Sie sicher, dass die geöffnete Ablaufverfolgungsdatei oder -tabelle die Ereignisklassen enthält, die für die Wiedergabe erforderlich sind. Weitere Informationen finden Sie unter [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  Klicken Sie im Ablaufverfolgungsfenster auf ein Ereignis.  
  
3.  Klicken Sie im Menü **Wiedergeben** auf **Ausführen bis Cursorposition**, und stellen Sie eine Verbindung zu dem Server her, auf dem Sie die Ablaufverfolgung wiedergeben möchten.  
  
4.  Überprüfen Sie im Dialogfeld **Wiedergabekonfiguration** die Einstellungen, und klicken Sie dann auf **OK**.  
  
     Die Wiedergabe beginnt; sie hält an, wenn sie die erste Cursorposition erreicht.  
  
5.  Drücken Sie F5, um die Ablaufverfolgung fortzusetzen.  
  
6.  Wiederholen Sie Schritt 5 bis zum Ende der Ablaufverfolgung.  
  
## Siehe auch  
 [Wiedergeben bis zu einem Breakpoint &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)   
 [Wiedergeben von Ablaufverfolgungen](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  