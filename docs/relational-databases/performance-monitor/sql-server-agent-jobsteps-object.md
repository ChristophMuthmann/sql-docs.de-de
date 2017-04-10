---
title: "SQL Server-Agent, Auftragsschritte-Objekt | Microsoft Docs"
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
  - "Auftragsschritte-Objekt"
  - "SQLAgent:Auftragsschritte"
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# SQL Server-Agent, Auftragsschritte-Objekt
  Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent: **Auftragsschritte** -Leistungsobjekt enthält Leistungsindikatoren, die Informationen zu den Auftragsschritten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents angeben. In der nachfolgenden Tabelle sind die in diesem Objekt enthaltenen Indikatoren aufgelistet.  
  
 Die folgende Tabelle enthält die Leistungsindikatoren von **SQLAgent:Auftragsschritte** .  
  
|Name|Beschreibung|  
|----------|-----------------|  
|**Aktive Schritte**|Dieser Indikator gibt die Anzahl der aktuell ausgeführten Auftragsschritte an.|  
|**Schritte in Warteschlange**|Dieser Indikator gibt die Anzahl der Auftragsschritte an, die für das Ausführen durch den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent bereitstehen, deren Ausführung jedoch noch nicht gestartet wurde.|  
|**Wiederholungen von Schritten gesamt**|Dieser Indikator gibt an, wie oft [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem letzten Serverneustart insgesamt versucht hat, einen Auftragsschritt neu zu starten.|  
  
 Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Instanz|Beschreibung|  
|--------------|-----------------|  
|**_Total**|Informationen für alle Auftragsschritte.|  
|**ActiveScripting**|Informationen für Auftragsschritte, die das **ActiveScripting** -Subsystem verwenden.|  
|**ANALYSISCOMMAND**|Informationen für Auftragsschritte, die das ANALYSISCOMMAND-Subsystem verwenden.|  
|**ANALYSISQUERY**|Informationen für Auftragsschritte, die das ANALYSISQUERY-Subsystem verwenden.|  
|**CmdExec**|Informationen für Auftragsschritte, die das **CmdExec** -Subsystem verwenden.|  
|**Distribution**|Informationen für Auftragsschritte, die das **Distribution** -Subsystem verwenden.|  
|**Dts**|Informationen für Auftragsschritte, die das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Subsystem verwenden.|  
|**LogReader**|Informationen für Auftragsschritte, die das **LogReader** -Subsystem verwenden.|  
|**Merge**|Informationen für Auftragsschritte, die das **Merge** -Subsystem verwenden.|  
|**PowerShell**|Informationen für Auftragsschritte, die das **PowerShell** -Subsystem verwenden.|  
|**QueueReader**|Informationen für Auftragsschritte, die das **QueueReader** -Subsystem verwenden.|  
|**Momentaufnahme**|Informationen für Auftragsschritte, die das **Momentaufnahme** -Subsystem verwenden.|  
|**TSQL**|Informationen für Auftragsschritte, die [!INCLUDE[tsql](../../includes/tsql-md.md)] ausführen.|  
  
## Siehe auch  
 [Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)   
 [Verwenden von Leistungsobjekten](../../ssms/agent/use-performance-objects.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  