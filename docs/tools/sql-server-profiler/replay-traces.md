---
title: Wiedergeben von Ablaufverfolgungen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, replaying traces
- Run to Cursor option
- Toggle Breakpoint option
- traces [SQL Server], replaying
- replaying traces
- playback engine [SQL Server Profiler]
- events [SQL Server], replaying traces
- Profiler [SQL Server Profiler], replaying traces
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98a09f67e8b39ad21c62bc2c793b5eb2b00e7a03
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="replay-traces"></a>Wiedergeben von Ablaufverfolgungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Bei der Wiedergabe handelt es sich um die Fähigkeit, Aktivitäten zu reproduzieren, die in einer Ablaufverfolgung aufgezeichnet wurden. Wenn Sie eine Ablaufverfolgung erstellen oder bearbeiten, können Sie sie in einer Datei speichern, um sie zu einem späteren Zeitpunkt wiederzugeben. Sie können mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] Ablaufverfolgungsaktivitäten von einem einzelnen Computer wiedergeben. Verwenden Sie für große Arbeitsauslastungen das Distributed Replay Utility, um Ablaufverfolgungsdaten von mehreren Computern wiederzugeben.  
  
 In diesem Abschnitt wird die Verwendung der Wiedergabefunktionen von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]beschrieben. Weitere Informationen zum Distributed Replay Utility finden Sie unter [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verfügt über ein Multithread-Wiedergabemodul, das Benutzerverbindungen und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung simulieren kann. Die Wiedergabe ist nützlich für die Behandlung von Anwendungs- oder Prozessproblemen. Wenn Sie das Problem identifiziert und Korrekturen implementiert haben, sollten Sie die Ablaufverfolgung, in der das mögliche Problem aufgetreten ist, für die korrigierte Anwendung bzw. den korrigierten Prozess ausführen. Geben Sie anschließend die ursprüngliche Ablaufverfolgung wieder, und vergleichen Sie die Ergebnisse.  
  
 Bei der Wiedergabe von Ablaufverfolgungen wird das Debuggen mithilfe der Optionen **Breakpoint ein/aus** und **Ausführen bis Cursorposition** im Menü [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Wiedergeben** unterstützt. Diese Optionen verbessern vor allem die Analyse von langen Skripts, weil sie die Wiedergabe der Ablaufverfolgung in kleine Segmente unterteilen können, damit sie schrittweise analysiert werden können.  
  
 Informationen zu den Berechtigungen, die zum Wiedergeben einer Ablaufverfolgung erforderlich sind, finden Sie unter [Erforderliche Berechtigungen zum Ausführen von SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Anforderungen für die Wiedergabe](../../tools/sql-server-profiler/replay-requirements.md)|Beschreibt die Ereignisse, die in einer Ablaufverfolgungsdefinition vorhanden sein müssen, damit die Ablaufverfolgung mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]wiedergegeben werden kann.|  
|[Wiedergabeoptionen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|Beschreibt die Optionen, die Sie im Dialogfeld **Wiedergabekonfiguration** von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]festlegen können.|  
|[Überlegungen zum Wiedergeben von Ablaufverfolgungen &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|Beschreibt Ablaufverfolgungsereignisse, die nicht mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] wiedergegeben werden können, und die Auswirkungen der Wiedergabe von Ablaufverfolgungen auf die Serverleistung.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
