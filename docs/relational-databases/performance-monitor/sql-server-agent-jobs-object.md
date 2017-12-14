---
title: SQL Server-Agent, Jobs-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 077245e1ece089fa0a0b4ef98f2dd1fa6b9ec0d9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server-Agent, Aufträge-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das **Jobs**-Leistungsobjekt des SQL Server-Agents enthält Leistungsindikatoren, die Informationen zu SQL Server-Agent-Aufträgen ausgeben. In der nachfolgenden Tabelle sind die in diesem Objekt enthaltenen Indikatoren aufgelistet.  
  
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
|**Sonstige**|Informationen zu Aufträgen, die nicht durch Warnungen oder Zeitpläne gestartet wurden. Meist werden diese Aufträge manuell mithilfe von **sp_start_job**gestartet.|  
|**Zeitpläne**|Informationen zu durch Zeitpläne gestarteten Aufträgen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Aufträgen](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [Verwenden von Leistungsobjekten](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
