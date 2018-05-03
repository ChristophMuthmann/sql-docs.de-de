---
title: Die Wiedergabe bis zu einer Cursorposition (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 723d3a47736b44dba88a50a2d24ed862c1f30507
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>Wiedergeben bis zu einer Cursorposition (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Artikel wird beschrieben, wie Ablaufverfolgungsdateien oder -tabellen mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] so wiedergegeben werden können, dass sie beim Erreichen einer Cursorposition angehalten werden. Durch das Anhalten von Ablaufverfolgungen an Cursorpositionen wird das Debugging erleichtert, da lange Ablaufverfolgungsskripts in kürzere Segmente unterteilt und inkrementell analysiert werden können.  
  
### <a name="to-replay-to-the-cursor"></a>So geben Sie bis zur Cursorposition wieder  
  
1.  Öffnen Sie die Ablaufverfolgungsdatei oder -tabelle, die Sie wiedergeben möchten. Weitere Informationen finden Sie unter [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) oder den Optimierungsratgeber von [Öffnen einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)die richtigen Ereignisse und Spalten aufgezeichnet werden.  
  
     Stellen Sie sicher, dass die geöffnete Ablaufverfolgungsdatei oder -tabelle die Ereignisklassen enthält, die für die Wiedergabe erforderlich sind. Weitere Informationen finden Sie unter [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  Klicken Sie im Ablaufverfolgungsfenster auf ein Ereignis.  
  
3.  Klicken Sie im Menü **Wiedergeben** auf **Ausführen bis Cursorposition**, und stellen Sie eine Verbindung zu dem Server her, auf dem Sie die Ablaufverfolgung wiedergeben möchten.  
  
4.  Überprüfen Sie im Dialogfeld **Wiedergabekonfiguration** die Einstellungen, und klicken Sie dann auf **OK**.  
  
     Die Wiedergabe beginnt; sie hält an, wenn sie die erste Cursorposition erreicht.  
  
5.  Drücken Sie F5, um die Ablaufverfolgung fortzusetzen.  
  
6.  Wiederholen Sie Schritt 5 bis zum Ende der Ablaufverfolgung.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wiedergeben bis zu einem Breakpoint &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)   
 [Wiedergeben von Ablaufverfolgungen](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
