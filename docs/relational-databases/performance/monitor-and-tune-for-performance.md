---
title: "&#220;berwachen und Optimieren der Leistung | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Instanzen von SQL Server, Überwachen der Leistung"
  - "Überwachen der Serverleistung [SQL Server]"
  - "Datenbankmodul [SQL Server], Leistung"
  - "Überwachen der Leistung [SQL Server], Informationen zu Leistung"
  - "Serverleistung [SQL Server]"
  - "Überwachen der Leistung [SQL Server]"
  - "Datenbankleistung [SQL Server], Informationen zu Leistung"
  - "Optimierung von Datenbanken [SQL Server], Informationen zu Leistung"
  - "Statusinformationen [SQL Server], Leistungsüberwachung"
  - "Datenbanküberwachung [SQL Server], Informationen zu Leistung"
  - "Überwachen [SQL Server], Abfrageleistung"
  - "Serverleistung [SQL Server], Informationen zu Leistung"
  - "Optimieren von Datenbanken [SQL Server]"
  - "Datenbankleistung [SQL Server]"
  - "Überwachen [SQL Server], Serverleistung"
  - "Datenbanküberwachung [SQL Server]"
  - "Überwachen der Serverleistung [SQL Server], Informationen zu Überwachung der Serverleistung"
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
caps.latest.revision: 35
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 35
---
# &#220;berwachen und Optimieren der Leistung
  Ziel der Überwachung von Datenbanken ist es, die Leistung eines Servers zu bewerten. Eine effektive Überwachung umfasst die regelmäßige Erstellung von Momentaufnahmen der aktuellen Leistung, um problematische Prozesse zu isolieren, und die kontinuierliche Sammlung von Daten, um Leistungstrends über längere Zeit zu verfolgen.  
  
 Durch die fortlaufende Auswertung der Datenbankleistung können Sie die Antwortzeiten minimieren und den Durchsatz maximieren, um so die optimale Leistung zu erzielen. Die effiziente Netzwerklast, Datenträger-E/A und CPU-Nutzung sind der Schlüssel zu Höchstleistungen. Hierzu müssen Sie die Anwendungsanforderungen gründlich analysieren, die logische und physische Struktur der Daten kennen, die Datenbanknutzung bewerten und Kompromisse zwischen gegensätzlichen Nutzungen, wie etwa OLTP (Online Transaction Processing) im Gegensatz zur Entscheidungsunterstützung, aushandeln.  
  
## Überwachen und Optimieren von Datenbanken für die Leistung  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Microsoft Windows stellen Hilfsprogramme bereit, mit denen der aktuelle Zustand der Datenbank angezeigt und die Leistung unter veränderten Bedingungen nachverfolgt werden kann. Es gibt eine Reihe von Tools und Methoden, mit denen Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überwachen können. Überwachen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht Ihnen Folgendes:  
  
-   Ermitteln, ob die Leistung verbessert werden kann. Indem Sie beispielsweise die Antwortzeiten für häufig verwendete Abfragen überwachen, können Sie ermitteln, ob Änderungen an der Abfrage oder den Indizes in den Tabellen erforderlich sind.  
  
-   Analysieren der Benutzeraktivität. Wenn Sie beispielsweise überwachen, wie Benutzer versuchen, eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen, können Sie ermitteln, ob die Sicherheit adäquat eingerichtet ist, und Anwendungen oder Entwicklungssysteme testen. Sie können beispielsweise durch Überwachen von SQL-Abfragen während der Ausführung ermitteln, ob sie richtig geschrieben sind und zu den erwarteten Ergebnissen führen.  
  
-   Beheben von Problemen oder Debuggen von Anwendungskomponenten, z. B. gespeicherte Prozeduren.  
  
## Überwachen in einer dynamischen Umgebung  
Geänderte Bedingungen bedeuten eine andere Leistung. In Ihren Auswertungen sehen Sie Leistungsänderungen, wenn die Anzahl der Benutzer steigt, wenn die Benutzer andere Zugriffs- und Verbindungsmethoden verwenden, wenn die Datenbank wächst, wenn andere Clientanwendungen genutzt werden, wenn sich die Daten in den Anwendungen ändern, wenn die Abfragen komplexer werden und wenn die Netzwerkbelastung ansteigt. Verwenden von Tools für die Leistungsüberwachung ermöglicht es Ihnen, Änderungen in der Leistung mit geänderten Bedingungen und komplexen Abfragen zu verknüpfen. **Beispiele:**:  
  
-   Wenn Sie die Antwortzeiten für häufig verwendete Abfragen überwachen, können Sie ermitteln, ob Änderungen an der Abfrage oder den Indizes in den Tabellen, in denen die Abfragen ausgeführt werden, notwendig sind.  
  
-   Sie können durch Überwachen von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfragen während der Ausführung ermitteln, ob die Abfragen richtig geschrieben sind und zu den erwarteten Ergebnissen führen.  
  
-   Wenn Sie überwachen, wie Benutzer versuchen, eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen, können Sie ermitteln, ob die Sicherheit adäquat eingerichtet ist, und Anwendungen und Entwicklungssysteme testen.  
  
 Die Antwortzeit ist die Zeitdauer, die benötigt wird, um die erste Zeile des Resultsets in Form einer optischen Bestätigung, dass eine Abfrage verarbeitet wird, an den Benutzer zurückzugeben. Der Durchsatz ist die Gesamtzahl der Abfragen, die vom Server während eines bestimmten Zeitraums bearbeitet werden.  
  
 Mit steigender Benutzerzahl nimmt auch der Wettstreit um die Ressourcen eines Servers zu, was wiederum zu einer erhöhten Antwortzeit und einem insgesamt reduzierten Durchsatz führt.  
  
## Überwachungs- und Leistungsoptimierungstasks  
  
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
  
## Siehe auch  
 [Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md)   
 [Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  