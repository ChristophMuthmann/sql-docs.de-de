---
title: "Überwachen und Optimieren der Leistung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f9825e46e8f39d8077df64a2e15b6a2eeec47c03
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-and-tune-for-performance"></a>Überwachen und Optimieren der Leistung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Ziel der Überwachung von Datenbanken ist, die Leistung eines Servers zu bewerten. Eine effektive Überwachung umfasst die regelmäßige Erstellung von Momentaufnahmen der aktuellen Leistung, um problematische Prozesse zu isolieren, und die kontinuierliche Sammlung von Daten, um Leistungstrends über längere Zeit zu verfolgen.  
  
 Durch die fortlaufende Auswertung der Datenbankleistung können Sie die Antwortzeiten minimieren und den Durchsatz maximieren, um so die optimale Leistung zu erzielen. Die effiziente Netzwerklast, Datenträger-E/A und CPU-Nutzung sind der Schlüssel zu Höchstleistungen. Hierzu müssen Sie die Anwendungsanforderungen gründlich analysieren, die logische und physische Struktur der Daten kennen, die Datenbanknutzung bewerten und Kompromisse zwischen gegensätzlichen Nutzungen, wie etwa OLTP (Online Transaction Processing) im Gegensatz zur Entscheidungsunterstützung, aushandeln.  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>Überwachen und Optimieren von Datenbanken für die Leistung  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Microsoft Windows stellen Hilfsprogramme bereit, mit denen der aktuelle Zustand der Datenbank angezeigt und die Leistung unter veränderten Bedingungen nachverfolgt werden kann. Es gibt eine Reihe von Tools und Methoden, mit denen Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]überwachen können. Überwachen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht Ihnen Folgendes:  
  
-   Ermitteln, ob die Leistung verbessert werden kann. Indem Sie beispielsweise die Antwortzeiten für häufig verwendete Abfragen überwachen, können Sie ermitteln, ob Änderungen an der Abfrage oder den Indizes in den Tabellen erforderlich sind.  
  
-   Analysieren der Benutzeraktivität. Wenn Sie beispielsweise überwachen, wie Benutzer versuchen, eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herzustellen, können Sie ermitteln, ob die Sicherheit adäquat eingerichtet ist, und Anwendungen oder Entwicklungssysteme testen. Sie können beispielsweise durch Überwachen von SQL-Abfragen während der Ausführung ermitteln, ob sie richtig geschrieben sind und zu den erwarteten Ergebnissen führen.  
  
-   Beheben von Problemen oder Debuggen von Anwendungskomponenten, z. B. gespeicherte Prozeduren.  
  
## <a name="monitoring-in-a-dynamic-environment"></a>Überwachen in einer dynamischen Umgebung  
Geänderte Bedingungen bedeuten eine andere Leistung. In Ihren Auswertungen sehen Sie Leistungsänderungen, wenn die Anzahl der Benutzer steigt, wenn die Benutzer andere Zugriffs- und Verbindungsmethoden verwenden, wenn die Datenbank wächst, wenn andere Clientanwendungen genutzt werden, wenn sich die Daten in den Anwendungen ändern, wenn die Abfragen komplexer werden und wenn die Netzwerkbelastung ansteigt. Verwenden von Tools für die Leistungsüberwachung ermöglicht es Ihnen, Änderungen in der Leistung mit geänderten Bedingungen und komplexen Abfragen zu verknüpfen. **Beispiele:**:  
  
-   Wenn Sie die Antwortzeiten für häufig verwendete Abfragen überwachen, können Sie ermitteln, ob Änderungen an der Abfrage oder den Indizes in den Tabellen, in denen die Abfragen ausgeführt werden, notwendig sind.  
  
-   Sie können durch Überwachen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen während der Ausführung ermitteln, ob die Abfragen richtig geschrieben sind und zu den erwarteten Ergebnissen führen.  
  
-   Wenn Sie überwachen, wie Benutzer versuchen, eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herzustellen, können Sie ermitteln, ob die Sicherheit adäquat eingerichtet ist, und Anwendungen und Entwicklungssysteme testen.  
  
 Die Antwortzeit ist die Zeitdauer, die benötigt wird, um die erste Zeile des Resultsets in Form einer optischen Bestätigung, dass eine Abfrage verarbeitet wird, an den Benutzer zurückzugeben. Der Durchsatz ist die Gesamtzahl der Abfragen, die vom Server während eines bestimmten Zeitraums bearbeitet werden.  
  
 Mit steigender Benutzerzahl nimmt auch der Wettstreit um die Ressourcen eines Servers zu, was wiederum zu einer erhöhten Antwortzeit und einem insgesamt reduzierten Durchsatz führt.  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>Überwachungs- und Leistungsoptimierungstasks  
  
|Thema| Task|  
|-----------|----------------------|  
|[Überwachen von SQL Server-Komponenten](../../relational-databases/performance/monitor-sql-server-components.md)|Erforderliche Schritte, um eine SQL Server-Komponente zu überwachen|  
|[Tools für die Leistungsüberwachung und -optimierung](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|Listet die Überwachungs- und Optimierungstools auf, die mit SQL Server verfügbar sind|  
|[Festlegen einer Leistungsbasislinie](../../relational-databases/performance/establish-a-performance-baseline.md)|Beschreibt, wie eine Leistungsbasislinie festgelegt wird|  
|[Isolieren von Leistungsproblemen](../../relational-databases/performance/isolate-performance-problems.md)|Isolieren von Leistungsproblemen bei Datenbanken|  
|[Identifizieren von Engpässen](../../relational-databases/performance/identify-bottlenecks.md)|Überwachen und Nachverfolgen der Serverleistung, um Engpässe zu ermitteln|  
|[Überwachen der Serverleistung und -aktivität](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|Verwenden von Leistungs- und Aktivitätsüberwachungstools von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und von Windows|  
|[Anzeigen und Speichern von Ausführungsplänen](../../relational-databases/performance/display-and-save-execution-plans.md)|Anzeigen und Speichern von Ausführungsplänen in einer Datei im XML-Format|  
|[Live-Abfragestatistik](../../relational-databases/performance/live-query-statistics.md)|Anzeigen von Echtzeitstatistiken zu den Ausführungsschritten einer Abfrage|  
|[Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|Verwenden von Abfragespeicher, um automatisch einen Verlauf der Abfragen, Pläne und Laufzeitstatistiken zu erfassen und diese zur Überprüfung aufzubewahren|  
|[Verwenden des Abfragespeichers mit In-Memory-OLTP](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)|Überlegungen zu speicheroptimierten Tabellen|  
|[Bewährte Methoden für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md)|Hinweise zur Verwendung des Abfragespeichers|  
  
## <a name="see-also"></a>Siehe auch  
 [Automatisierte Verwaltung in einem Unternehmen](http://msdn.microsoft.com/library/44d8365b-42bd-4955-b5b2-74a8a9f4a75f)   
 [Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
