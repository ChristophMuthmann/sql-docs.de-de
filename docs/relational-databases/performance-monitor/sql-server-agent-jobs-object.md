---
title: "SQL Server-Agent, Auftr&#228;ge-Objekt | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLAgent:Aufträge"
  - "Aufträge-Objekt"
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# SQL Server-Agent, Auftr&#228;ge-Objekt
  Das **Jobs** -Leistungsobjekt des SQL Server-Agents enthält Leistungsindikatoren, die Informationen zu SQL Server-Agent-Aufträgen ausgeben. In der nachfolgenden Tabelle sind die in diesem Objekt enthaltenen Indikatoren aufgelistet.  
  
 Die nachfolgende Tabelle enthält die **SQLAgent:Jobs** -Leistungsindikatoren.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|**Aktive Aufträge**|Dieser Leistungsindikator erfasst die Anzahl der gerade ausgeführten Aufträge.|  
|**Fehlerhafte Aufträge**|Dieser Leistungsindikator erfasst die Anzahl der Aufträge, die mit einem Fehler beendet wurden.|  
|**Erfolgsquote der Aufträge**|Dieser Leistungsindikator gibt den Prozentsatz der erfolgreich abgeschlossenen Aufträge aus.|  
|**Aktivierte Aufträge/Minute**|Dieser Leistungsindikator gibt die Anzahl der Aufträge aus, die innerhalb der letzten Minute gestartet wurden.|  
|**Aufträge in Warteschlange**|Dieser Leistungsindikator gibt die Anzahl der Aufträge aus, die zur Ausführung durch den SQL Server-Agent bereitstehen, jedoch noch nicht gestartet wurden.|  
|**Erfolgreiche Aufträge**|Dieser Leistungsindikator erfasst die Anzahl der Aufträge, die erfolgreich beendet wurden.|  
  
 Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Instanz|Beschreibung|  
|--------------|-----------------|  
|**_Total**|Informationen zu allen Aufträgen.|  
|**Warnungen**|Informationen zu durch Warnungen gestarteten Aufträgen.|  
|**Sonstige**|Informationen zu Aufträgen, die nicht durch Warnungen oder Zeitpläne gestartet wurden. Meist werden diese Aufträge manuell mithilfe von **sp_start_job** gestartet.|  
|**Zeitpläne**|Informationen zu durch Zeitpläne gestarteten Aufträgen.|  
  
## Siehe auch  
 [Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)   
 [Verwenden von Leistungsobjekten](../../ssms/agent/use-performance-objects.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  