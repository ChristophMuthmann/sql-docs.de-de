---
title: "SQL Server, &#39;Statistiken f&#252;r Arbeitsauslastungsgruppen&#39;-Objekt | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/04/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Statistiken für Arbeitsauslastungsgruppen-Objekt"
  - "SQLServer:Statistiken für Arbeitsauslastungsgruppen"
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server, &#39;Statistiken f&#252;r Arbeitsauslastungsgruppen&#39;-Objekt
  Das SQLServer:Statistiken für Arbeitsauslastungsgruppen-Objekt enthält Leistungsindikatoren, die Informationen zur Ressourcenkontrollen-Arbeitsauslastungsgruppenstatistik zurückgeben.  
  
 Jede aktive Arbeitsauslastungsgruppe erstellt eine Instanz des Leistungsobjekts SQLServer:Statistiken für Arbeitsauslastungsgruppen, wobei der Name der Instanz dem Namen der Arbeitsauslastungsgruppe in der Ressourcenkontrolle entspricht. In der folgenden Tabelle sind die für diese Instanz unterstützten Leistungsindikatoren beschrieben.  
  
|Indikatorname|Beschreibung|  
|------------------|-----------------|  
|**Aktive parallele Threads**|Die aktuelle Anzahl belegter paralleler Threads.|  
|**Aktive Anforderungen**|Die Anzahl von Anforderungen, die aktuell in dieser Arbeitsauslastungsgruppe ausgeführt werden. Diese Anzahl sollte der Anzahl von Zeilen entsprechen, die anhand der Gruppen-ID aus sys.dm_exec_requests herausgefiltert wird.|  
|**Blockierte Anforderungen**|Die aktuelle Anzahl blockierter Anforderungen in der Arbeitsauslastungsgruppe. Mit diesem Wert können Arbeitsauslastungseigenschaften ermittelt werden.|  
|**CPU verzögert %**|System-CPU verzögert für alle Anforderungen in der angegebenen Instanz des Leistungsobjekts als Prozentsatz der gesamten aktiven Zeit.| 
|**Basis für CPU verzögert %**|Nur zur internen Verwendung.| 
|**CPU effektiv %**|System-CPU-Verwendung für alle Anforderungen in der angegebenen Instanz des Leistungsobjekts als Prozentsatz der gesamten aktiven Zeit.| 
|**Basis für CPU effektiv %**|Nur zur internen Verwendung.| 
|**CPU-Verwendung in %**|Die von allen Anforderungen in dieser Arbeitsauslastungsgruppe belegte CPU-Bandbreite, gemessen relativ zum Computer und normalisiert auf alle CPUs im System. Dieser Wert ändert sich, wenn sich die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess verfügbare CPU-Leistung ändert. Der Wert wird auf die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess empfangenen Elemente normalisiert.| 
|**Basis für CPU-Verwendung in %**|Nur zur internen Verwendung.| 
|**CPU-Verletzung %**|Der Unterschied zwischen der CPU-Reservierung und dem effektiv für Zeitplanung aufgewendeten Prozentsatz.|  
|**Maximale CPU-Zeit für Anforderungen (ms)**|Die maximal von einer aktuell in der Arbeitsauslastungsgruppe ausgeführten Anforderung belegte CPU-Zeit in Millisekunden.|  
|**Maximale Arbeitsspeicherzuweisung für Anforderungen (KB)**|Der maximale Wert der Arbeitsspeicherzuweisung für eine Abfrage in Kilobyte (KB).|  
|**Abfrageoptimierungen/Sekunde**|Die Anzahl von Abfrageoptimierungen, die pro Sekunde in dieser Arbeitsauslastungsgruppe stattgefunden haben. Mit diesem Wert können Arbeitsauslastungseigenschaften ermittelt werden.|  
|**Anforderungen in der Warteschlange**|Die aktuelle Anzahl der Anforderungen in der Warteschlange, die darauf warten, abgerufen zu werden. Diese Anzahl kann ungleich 0 (null) sein, wenn eine Einschränkung angewandt wird, nachdem der Grenzwert GROUP_MAX_REQUESTS erreicht wurde.|  
|**Reduzierte Arbeitsspeicherzuweisungen/Sekunde**|Die Anzahl von Abfragen, die nicht die optimale Menge an Arbeitsspeicherzuweisungen pro Sekunde erhalten.|  
|**Abgeschlossene Anforderungen/Sekunde**|Die Anzahl der in dieser Arbeitsauslastungsgruppe abgeschlossenen Anforderungen. Diese Anzahl ist kumulativ.|  
|**Suboptimale Pläne/Sekunde**|Die Anzahl von suboptimalen Plänen, die pro Sekunde in dieser Arbeitsauslastungsgruppe erzeugt werden.|  
  
## Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, 'Statistiken für Ressourcenpools'-Objekt](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)  
  
  