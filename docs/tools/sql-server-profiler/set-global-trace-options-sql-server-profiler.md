---
title: Festlegen globaler Ablaufverfolgungsoptionen (SQL Server Profiler) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: global trace options [SQL Server]
ms.assetid: 2854608a-c3c7-4eb8-b567-034bfec4b1a9
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffb801e92dfaa141be2b5e942a1c0bd95c19a6cb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="set-global-trace-options-sql-server-profiler"></a>Festlegen globaler Ablaufverfolgungsoptionen (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In diesem Thema wird beschrieben, wie zum Festlegen von Optionen, die für alle ablaufverfolgungen gelten, die mit einer bestimmten Instanz von erstellt werden [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-set-global-trace-options"></a>So legen Sie globale Ablaufverfolgungsoptionen fest  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Klicken Sie im Dialogfeld **Allgemeine Optionen**auf **Schriftart auswählen**, um die Anzeigeoptionen zu ändern, und klicken Sie anschließend auf **OK**.  
  
3.  Sie können optional auch **Ablaufverfolgung sofort nach Herstellen der Verbindung starten**auswählen.  
  
4.  Sie können optional auch **Ablaufverfolgungsdefinition bei Änderung der Anbieterversion aktualisieren**auswählen. Diese Option wird empfohlen, und sie ist standardmäßig aktiviert. Wenn diese Option aktiviert ist, wird die Ablaufverfolgungsdefinition automatisch auf die aktuelle Version des Servers aktualisiert, auf dem die Ablaufverfolgung ausgeführt wird.  
  
5.  Sie können optional angeben, wie der Server mit Rolloverdateien umgehen soll:  
  
    -   Wählen Sie **Alle Rolloverdateien nacheinander ohne Eingabeaufforderung laden** aus, damit Rolloverdateien während der Wiedergabe automatisch geladen werden.  
  
    -   Wählen sie **Bestätigung vor dem Laden von Rolloverdateien** aus, um Rolloverdateien während der Wiedergabe steuern zu können.  
  
    -   Wählen Sie **Nachfolgende Rolloverdateien niemals laden** aus, um jeweils nur eine Datei wiederzugeben.  
  
6.  Optional können Sie die Wiedergabeoptionen festlegen:  
  
    -   **Standardanzahl von Wiedergabethreads** wird die Anzahl von Prozessorthreads kontrolliert, die während der Wiedergabe verwendet werden sollen. Durch eine höhere Anzahl von Threads wird die Wiedergabe schneller abgeschlossen. Die Serverleistung wird während der Wiedergabe jedoch beeinträchtigt. Die empfohlene Einstellung lautet **4**. Die folgende Tabelle enthält die verfügbaren Optionen:  
  
        |value|Description|  
        |-----------|-----------------|  
        |**2**|Minimalwert. Verwenden von zwei Threads für die Wiedergabe.|  
        |**4**|Standardwert.|  
        |**255**|Maximalwert. Durch Einstellung eines Maximalwerts wird die für andere Prozesse verfügbare Leistung eingeschränkt.|  
  
    -   Mit**Standardwartezeit für Systemüberwachung (Sek.)** wird die maximale Zeitspanne in Sekunden angegeben, über die ein Wiedergabethread einen anderen Prozess blockieren kann. In der folgenden Tabelle werden die einzelnen Werten näher erläutert.  
  
        |value|Description|  
        |-----------|-----------------|  
        |**0**|Minimalwert. Die Einstellung **0** bedeutet, dass [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] einen blockierenden Prozess in keinem Fall beendet.|  
        |**3600**|Standardwert. Lässt blockierende Prozesse zu, die nicht länger als **3600** Sekunden oder eine Stunde dauern.|  
        |**86400**|Maximalwert. Lässt blockierende Prozesse zu, die nicht länger als **86400** Sekunden oder einen Tag dauern.|  
  
    -   Mit**Standardabrufintervall für Systemüberwachung (Sek.)** wird die Frequenz festgelegt, mit der Wiedergabethreads für blockierende Prozesse abgerufen werden. In der folgenden Tabelle werden die einzelnen Werten näher erläutert.  
  
        |value|Description|  
        |-----------|-----------------|  
        |**1**|Minimalwert. Eine Einstellung von **1** bedeutet, dass [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] blockierende Prozesse einmal pro Sekunde abruft.|  
        |**60**|Standardwert. Abrufen von blockierenden Prozessen einmal pro Minute.|  
        |**86400**|Maximalwert. Abrufen von blockierenden Prozessen einmal pro **86400** Sekunden, oder einmal pro Tag.|  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen der Standardeinstellungen für die Ablaufverfolgungsanzeige &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
