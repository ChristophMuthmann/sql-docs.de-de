---
title: "SQL Server, Plancache-Objekt | Microsoft Docs"
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
  - "Plancache-Objekt"
  - "SQLServer:Plancache"
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# SQL Server, Plancache-Objekt
  Das **Plancache** -Objekt stellt Indikatoren bereit, mit denen überwacht werden kann, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Arbeitsspeicher zum Speichern von Objekten verwendet, z. B. gespeicherten Prozeduren, Ad-hoc-Anweisungen, vorbereiteten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen sowie Triggern. Es können mehrere Instanzen des **Plancache** -Objekts gleichzeitig überwacht werden, wobei jede Instanz einen unterschiedlichen Typ von zu überwachendem Plan darstellt.  
  
 In dieser Tabelle werden die **SQLServer:Plancache**Leistungsindikatoren beschrieben.  
  
|SQL Server, Plancache-Leistungsindikatoren|Beschreibung|  
|------------------------------------|-----------------|  
|**Cachetrefferquote**|Das Verhältnis zwischen Cachetreffern und -suchvorgängen.|  
|**Basis für Cachetrefferquote**|Nur zur internen Verwendung.| 
|**Cacheobjektzähler**|Anzahl der Cacheobjekte im Cache.|  
|**Cacheseiten**|Anzahl der von Cacheobjekten verwendeten 8-KB-Seiten.|  
|**Verwendete Cacheobjekte**|Anzahl der verwendeten Cacheobjekte.|  
  
 Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Plancache-Instanz|Beschreibung|  
|-------------------------|-----------------|  
|**_Total**|Informationen zu allen Typen von Cacheinstanzen.|  
|**Sql-Pläne**|Abfragepläne, die von einer Ad-hoc-[!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage, einschließlich automatisch parametrisierten Abfragen, oder durch [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen generiert wurden, die mit **sp_prepare** oder **sp_cursorprepare** vorbereitet wurden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichert die Pläne für Ad-hoc- [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen für die spätere Wiederverwendung zwischen, wenn die identische [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung später ausgeführt wird. Vom Benutzer parametrisierte Abfragen (selbst wenn sie nicht ausdrücklich vorbereitet sind) werden ebenfalls mit Prepared SQL Plans überwacht.|  
|**Objektpläne**|Abfragepläne, die durch Erstellen von gespeicherten Prozeduren, Funktionen oder Triggern generiert wurden.|  
|**Gebundene Strukturen**|Normalisierte Strukturen für Sichten, Regeln, berechnete Spalten und CHECK-Einschränkungen.|  
|**Erweiterte gespeicherte Prozeduren**|Kataloginformationen für erweiterte Prozeduren.|  
|**Temporäre Tabellen & Tabellenvariablen**|Cacheinformationen zu temporären Tabellen und Tabellenvariablen.|  
  
## Siehe auch  
 [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, Puffer-Manager-Objekt](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  