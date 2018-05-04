---
title: Einführung in die Überwachung von Analysis Services mit SQL Server Profiler | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9ea003dafa721277f7562696f4b6be254d281be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>Einführung in die Überwachung von Analysis Services mit SQL Server Profiler
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] können Sie Ereignisse überwachen, die von einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]generiert werden. Mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]können folgende Aktionen ausgeführt werden:  
  
-   Überwachen der Leistung einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Debuggen von MDX-Anweisungen (Multidimensional Expressions).  
  
-   Identifizieren von MDX-Anweisungen, die langsam ausgeführt werden.  
  
-   Testen von MDX-Anweisungen in der Entwicklungsphase eines Projekts durch schrittweises Durchlaufen von Anweisungen, um die ordnungsgemäße Funktionsweise des Codes zu bestätigen.  
  
-   Problembehandlungen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durch Aufzeichnen von Ereignissen auf einem Produktionssystem und Wiedergeben dieser aufgezeichneten Ereignisse in einem Testsystem. Diese Methode ist hilfreich beim Testen und Debuggen, da die Benutzer das Produktionssystem störungsfrei weiterverwenden können.  
  
-   Überwachen und Analysieren der Aktivität, die in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]aufgetreten ist. Sicherheitsadministratoren können jedes der überwachten Ereignisse überprüfen. Hierzu zählen erfolgreiche oder fehlgeschlagene Anmeldeversuche sowie erfolgreiche oder fehlgeschlagene Berechtigungen für den Zugriff auf Anweisungen und Objekte.  
  
-   Anzeigen von Daten zu den erfassten Ereignissen auf dem Bildschirm oder Erfassen und Speichern von Daten zu jedem Ereignis in einer Datei oder einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle, um sie zu einem späteren Zeitpunkt zu analysieren oder wiederzugeben. Bei der Wiedergabe von Daten können Sie die gespeicherten Ereignisse so, wie sie ursprünglich auftraten, entweder in Echtzeit oder Schritt für Schritt erneut ausführen.  
  
## <a name="using-sql-server-profiler"></a>Verwenden von SQL Server Profiler  
 Damit Sie mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] Ablaufverfolgungen erstellen oder wiedergeben können, müssen Sie Mitglied der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Serverrolle sein. Mitglieder der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Serverrolle können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] über die Programmgruppe [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Menü **Start** starten.  
  
 Beachten Sie beim Verwenden von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]Folgendes:  
  
-   Ablaufverfolgungsdefinitionen werden in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mit der CREATE-Anweisung gespeichert.  
  
-   Mehrere Ablaufverfolgungen können gleichzeitig ausgeführt werden.  
  
-   Mehrere Verbindungen können Ereignisse aus derselben Ablaufverfolgung erhalten.  
  
-   Eine Ablaufverfolgung kann nach Beenden und Neustarten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fortgesetzt werden.  
  
    > [!NOTE]  
    >  Kennwörter werden in Ablaufverfolgungsereignissen nicht offen gelegt, sondern im Ereignis durch ****** ersetzt.  
  
 Sie sollten mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] nur Ereignisse überwachen, an denen Sie am meisten interessiert sind, um eine optimale Leistung zu erreichen. Wenn zu viele Ereignisse überwacht werden, nimmt der Verwaltungsaufwand zu, und die Ablaufverfolgungsdatei oder -tabelle kann sehr groß werden, vor allem, wenn über längere Zeit überwacht wird. Verwenden Sie außerdem Filter, um die Menge der gesammelten Daten zu begrenzen und zu verhindern, dass Ablaufverfolgungen zu groß werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [Erstellen von Profilerablaufverfolgungen für Replay & #40; Analysis Services & #41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)  
  
  
