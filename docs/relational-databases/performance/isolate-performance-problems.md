---
title: "Isolieren von Leistungsproblemen | Microsoft Docs"
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
  - "Eingrenzen von Leistungsproblemen [SQL Server]"
  - "Überwachen der Leistung [SQL Server], Isolieren von Problemen"
  - "Datenbanküberwachung [SQL Server], Isolieren von Problemen"
  - "Optimieren von Datenbanken [SQL Server], Isolieren von Problemen"
  - "Überwachen der Serverleistung [SQL Server], Isolieren von Problemen"
  - "Datenbankleistung [SQL Server], Isolieren von Problemen"
  - "Serverleistung [SQL Server], Isolieren von Problemen"
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# Isolieren von Leistungsproblemen
  Häufig ist es effektiver, zur Isolierung von Leistungsproblemen bei Datenbanken mehrere [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tools oder Microsoft Windows-Tools gleichzeitig zu verwenden. So können Sie beispielsweise mithilfe der Funktion für den grafischen Ausführungsplan (auch Showplan genannt) Deadlocks in einer einzigen Abfrage erkennen. Einige andere Leistungsprobleme lassen sich wiederum einfacher ermitteln, indem Sie die Überwachungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Windows zusammen verwenden.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] kann für die Überwachung und Problembehandlung von Transact-SQL-Anweisungen und anwendungsbasierten Problemen verwendet werden. Mit dem Systemmonitor können Sie Hardwareprobleme und andere systembedingte Probleme überwachen.  
  
 Sie können die folgenden Bereiche zur Problembehandlung überwachen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungsbatches, die von Benutzeranwendungen übermittelt wurden.  
  
-   Benutzeraktivität, z. B. Sperren oder Deadlocks.  
  
-   Hardwareaktivität, z. B. die Datenträgernutzung.  
  
 Mögliche Probleme sind:  
  
-   Fehler bei der Anwendungsentwicklung im Zusammenhang mit fehlerhaft geschriebenen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   Hardwarefehler, z. B. Fehler im Zusammenhang mit den Datenträgern oder dem Netzwerk.  
  
-   Zu häufiges Blockieren aufgrund einer fehlerhaft entworfenen Datenbank.  
  
## Tools für häufig auftretende Leistungsprobleme  
 Genau so wichtig ist die sorgfältige Auswahl der Leistungsprobleme, die durch die einzelnen Tools überwacht oder optimiert werden sollen. Welches Tool und welcher Dienst geeignet sind, hängt von der Art des zu lösenden Leistungsproblems ab.  
  
 Die folgenden Themen enthalten Beschreibungen einer Vielzahl von Tools zur Überwachung und Optimierung sowie der durch sie feststellbaren Probleme.  
  
 [Identifizieren von Engpässen](../../relational-databases/performance/identify-bottlenecks.md)  
  
 [Überwachen der Speicherauslastung](../../relational-databases/performance-monitor/monitor-memory-usage.md)  
  
  