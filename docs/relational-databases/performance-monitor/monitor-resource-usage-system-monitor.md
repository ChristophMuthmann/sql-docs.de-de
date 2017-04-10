---
title: "&#220;berwachen der Ressourcenverwendung (Systemmonitor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachen der Leistung [SQL Server], Ressourcennutzung"
  - "Systemmonitor [SQL Server], Informationen zu Windows-Systemmonitor"
  - "Ressourcenverwendung überwachen [SQL Server]"
  - "Systemmonitor [SQL Server]"
  - "Indikatoren [SQL Server], Themenbereich Ressourcenverwendung"
  - "Leistungsindikatoren [SQL Server], Themenbereich Ressourcenverwendung"
  - "Windows-Systemmonitor [SQL Server], Informationen zu Windows-Systemmonitor"
  - "Überwachen [SQL Server], Nutzung von Serverressourcen"
  - "Überwachen der Ressourcenverwendung [SQL Server]"
  - "Windows-Systemmonitor [SQL Server]"
  - "Datenbanküberwachung [SQL Server], Ressourcennutzung"
  - "Datenbankleistung [SQL Server], Ressourcennutzung"
  - "Optimieren von Datenbanken [SQL Server], Ressourcennutzung"
  - "Serverleistung [SQL Server], Ressourcennutzung"
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# &#220;berwachen der Ressourcenverwendung (Systemmonitor)
  Wenn Sie das Microsoft Windows-Serverbetriebssystem ausführen, können Sie das grafische Tool Systemmonitor verwenden, um die Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu messen. Es ist möglich, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekte, Leistungsindikatoren und das Verhalten anderer Objekte anzuzeigen, wie z. B. Prozessoren, Arbeitsspeicher, Cache, Threads und Prozesse. Jedes dieser Objekte verfügt über eine zugeordnete Gruppe von Leistungsindikatoren, durch die die Geräteverwendung, Länge von Warteschlangen, Wartezeiten sowie andere Indikatoren für den Durchsatz und die interne Auslastung ermittelt werden können.  
  
> [!NOTE]  
>  Der Systemmonitor wurde nach Windows NT 4.0 grundlegend aktualisiert.  
  
## Vorteile des Systemmonitors  
 Der Systemmonitor kann dazu genutzt werden, die Leistungsindikatoren des Windows-Betriebssystems und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gleichzeitig zu überwachen, um Zusammenhänge zwischen der Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Windows zu ermitteln. Wenn Sie beispielsweise die Datenträger-E/A-Leistungsindikatoren von Windows und die Leistungsindikatoren des Puffer-Managers von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gleichzeitig überwachen, können Sie sich einen Überblick über das Verhalten des gesamten Systems verschaffen.  
  
 Mit dem Systemmonitor können Sie Statistiken über die aktuelle Aktivität und Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abrufen. Der Systemmonitor ermöglicht Folgendes:  
  
-   Gleichzeitiges Anzeigen von Daten einer beliebigen Anzahl von Computern  
  
-   Anzeigen und Ändern von Diagrammen, um die aktuelle Aktivität wiederzugeben, sowie Anzeigen von Leistungsindikatorwerten, die in der vom Benutzer definierten Häufigkeit aktualisiert werden  
  
-   Exportieren von Daten aus Diagrammen, Protokollen, Warnungsprotokollen und Berichten in Tabellen- oder Datenbankanwendungen, um sie weiter zu bearbeiten oder zu drucken  
  
-   Hinzufügen von Systemwarnungen, die ein Ereignis im Warnungsprotokoll einfügen und über die Sie durch das Ausgeben einer Netzwerkwarnung benachrichtigt werden können  
  
-   Ausführen einer vordefinierten Anwendung, wenn ein Leistungsindikatorwert zum ersten Mal einen benutzerdefinierten Wert über- bzw. unterschreitet oder jedes Mal, wenn dies geschieht  
  
-   Erstellen von Protokolldateien, die Daten über verschiedene Objekte von unterschiedlichen Computern enthalten  
  
-   Anfügen von ausgewählten Abschnitten aus anderen bestehenden Protokolldateien an eine Datei, um ein Langzeitarchiv zu erstellen  
  
-   Anzeigen von aktuellen Aktivitätsberichten oder Erstellen von Berichten anhand bestehender Protokolldateien  
  
-   Sichern von einzelnen Diagramm-, Warnungs-, Protokoll- oder Berichtseinstellungen oder der gesamten Einrichtung des Arbeitsbereichs für die spätere Wiederverwendung  
  
    > [!NOTE]  
    >  Ab Windows NT 4.0 wurde der Leistungsindikator durch den Systemmonitor ersetzt. Diese Tasks können Sie mit dem Systemmonitor oder mit dem Leistungsindikator ausführen.  
  
## Leistung des Systemmonitors  
 Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und das Betriebssystem Microsoft Windows überwachen, um Leistungsprobleme näher zu untersuchen, sollten Sie sich dabei zunächst auf drei Hauptbereiche konzentrieren:  
  
-   Datenträgeraktivität  
  
-   Prozessornutzung  
  
-   Speicherauslastung  
  
 Die Überwachung eines Computers, auf dem der Systemmonitor ausgeführt wird, kann die Computerleistung geringfügig beeinträchtigen. Sie sollten deshalb die Daten des Systemmonitors auf einem anderen Datenträger oder einem anderen Computer protokollieren, damit die Auswirkungen auf den überwachten Computer reduziert werden. Oder führen Sie den Systemmonitor von einem Remotecomputer aus. Darüber hinaus sollten Sie nur die Leistungsindikatoren überwachen, an denen Sie interessiert sind. Wenn Sie zu viele Leistungsindikatoren überwachen, wird der Überwachungsprozess um den Verwaltungsaufwand der Ressourcenverwendung erhöht und die Leistung des überwachten Computers beeinträchtigt.  
  
## Tasks des Systemmonitors  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt die Verwendung des Systemmonitors und erläutert den Leistungsaufwand beim Einsatz des Systemmonitors.|[Ausführen des Systemmonitors](../../relational-databases/performance-monitor/run-system-monitor.md)|  
|Beschreibt die Überwachung der Leistungsindikatoren eines Datenträgers zur Ermittlung der Datenträgeraktivität und der Menge von E/A, die von den SQL Server-Komponenten generiert wird.|[Überwachen der Datenträgerverwendung](../../relational-databases/performance-monitor/monitor-disk-usage.md)|  
|Beschreibt die Überwachung einer Instanz von Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Feststellung, ob sich die CPU-Nutzungsraten im Normalbereich bewegen.|[Überwachen der CPU-Auslastung](../../relational-databases/performance-monitor/monitor-cpu-usage.md)|  
|Beschreibt die Überwachung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Bestätigung einer Speicherauslastung im normalen Bereich.|[Überwachen der Speicherauslastung](../../relational-databases/performance-monitor/monitor-memory-usage.md)|  
|Beschreibt das Erstellen einer Warnung, die ausgelöst wird, sobald ein Schwellenwert für einen Leistungsindikator des Systemmonitors erreicht wird.|[Erstellen einer SQL Server-Datenbankwarnung](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)|  
|Beschreibt das Erstellen von Diagrammen, Warnungen, Protokollen und Berichten für die Überwachung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Erstellen von Diagrammen, Warnungen, Protokollen und Berichten](../../relational-databases/performance-monitor/create-charts-alerts-logs-and-reports.md)|  
|Führt Objekte und Leistungsindikatoren auf, die der Systemmonitor zur Überwachung der Aktivität von Computern, die eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen, nutzt.|[Verwenden von SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md)|  
|Enthält eine Liste der Objekte und Leistungsindikatoren, die vom Systemmonitor zur Überwachung von In-Memory OLTP-Aktivitäten verwendet werden.|[Leistungsindikatoren für SQL Server XTP &#40;In-Memory-OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)|  
  
  