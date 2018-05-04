---
title: Wiedergeben einer Ablaufverfolgungsdatei (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 9e361275-c8fd-4499-8389-242cf8e27415
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e32aac4b840db94bc1698d9e1b8eb680fb22866
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="replay-a-trace-file-sql-server-profiler"></a>Wiedergeben einer Ablaufverfolgungsdatei (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Wiedergabe bezeichnet die Möglichkeit, eine gespeicherte Ablaufverfolgung zu öffnen und erneut wiederzugeben. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verfügt über ein Multithread-Wiedergabemodul, das Benutzerverbindungen und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung simulieren kann. Die Wiedergabe ist nützlich für die Behandlung von Anwendungs- oder Prozessproblemen. Wenn Sie das Problem identifiziert und Korrekturen implementiert haben, sollten Sie die Ablaufverfolgung, in der das mögliche Problem aufgetreten ist, für die korrigierte Anwendung bzw. den korrigierten Prozess erneut ausführen. Geben Sie anschließend die ursprüngliche Ablaufverfolgung wieder, und vergleichen Sie die Ergebnisse.  
  
 Neben anderen Ereignisklassen, die Sie überwachen möchten, müssen bestimmte Ereignisklassen erfasst werden, um die Wiedergabe zu ermöglichen. Diese Ereignisse werden standardmäßig erfasst, wenn Sie die **TSQL_Replay** -Ablaufverfolgungsvorlage verwenden. Weitere Informationen finden Sie unter [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
### <a name="to-replay-a-trace-file"></a>So geben Sie eine Ablaufverfolgungsdatei wieder  
  
1.  Zeigen Sie im Menü **Datei** auf **Öffnen**, und klicken Sie dann auf **Ablaufverfolgungsdatei**. Wählen Sie eine Ablaufverfolgungsdatei aus, die die für die Wiedergabe erforderlichen Ereignisklassen enthält.  
  
2.  Klicken Sie im Menü **Wiedergeben** auf **Start**, und stellen Sie eine Verbindung mit der Serverinstanz her, in der Sie die Ablaufverfolgung wiedergeben möchten.  
  
3.  Geben Sie im Dialogfeld **Wiedergabekonfiguration** auf der Registerkarte **Grundlegende Wiedergabeoptionen** den **Wiedergabeserver**an. Klicken Sie auf **Ändern** , um den im Feld **Wiedergabeserver** angezeigten Server zu ändern.  
  
4.  Wählen Sie optional eines der folgenden Ziele zum Speichern der Wiedergabe aus:  
  
    -   **In Datei speichern**gibt eine Datei an, in der die Wiedergabe gespeichert wird.  
  
    -   **In Tabelle speichern**gibt eine Tabelle an, in der die Wiedergabe gespeichert wird.  
  
5.  Wählen Sie entweder **Ereignisse in der Reihenfolge wiedergeben, in der ihr Ablauf verfolgt wurde**oder **Ereignisse mithilfe mehrerer Threads wiedergeben**. In der folgenden Tabelle wird der Unterschied zwischen diesen Einstellungen beschrieben.  
  
    |Option|Description|  
    |------------|-----------------|  
    |**Ereignisse in der Reihenfolge wiedergeben, in der ihr Ablauf verfolgt wurde**|Gibt Ereignisse in der Reihenfolge wieder, in der sie aufgezeichnet wurden. Diese Option aktiviert das Debuggen.|  
    |**Ereignisse mithilfe mehrerer Threads wiedergeben**|Diese Option verwendet mehrere Threads, um die einzelnen Ereignisse unabhängig von der Reihenfolge wiederzugeben. Diese Option optimiert die Leistung.|  
  
6.  Wählen Sie **Wiedergabeergebnisse anzeigen** aus, um die Wiedergabe während des Auftretens anzuzeigen.  
  
7.  Klicken Sie optional auf die Registerkarte **Erweiterte Wiedergabeoptionen**, um folgende Optionen zu konfigurieren:  
  
    -   Wählen Sie **System-SPIDs wiedergeben**aus, um alle Serverprozess-IDs (SPIDs) wiederzugeben.  
  
    -   Wählen Sie **Nur eine SPID wiedergeben**aus, um die Wiedergabe auf Prozesse zu beschränken, die zu einer bestimmten SPID gehören. Geben Sie im Feld **SPID für Wiedergabe** die SPID ein.  
  
    -   Wählen Sie **Wiedergabe nach Datum und Zeit beschränken**aus, um Ereignisse wiederzugeben, die in einem bestimmten Zeitraum aufgetreten sind. Wählen Sie ein Datum und eine Uhrzeit für **Startzeit**und **Beendigungszeit**aus, um den in der Wiedergabe enthaltenen Zeitraum anzugeben.  
  
    -   Konfigurieren Sie **Systemüberwachungsoptionen**, um zu steuern, wie SQL Server die Prozesse während der Wiedergabe verwaltet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erforderliche Berechtigungen zum Ausführen von SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Wiedergeben von Ablaufverfolgungen](../../tools/sql-server-profiler/replay-traces.md)   
 [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
