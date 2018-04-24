---
title: 'SQL Server: Buffer Node | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6da0672f20d4f5ded385bc8bbc709030fc3b9c8f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-serverbuffer-node"></a>SQLServer: Buffer Node
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das **Buffer Node** -Objekt stellt Leistungsindikatoren bereit, die vom **Puffer-Manager** -Objekt bereitgestellte Leistungsindikatoren ergänzen. Es ermöglicht Ihnen die Überwachung der Seitenverteilung im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Pufferpool für jeden NUMA-Knoten (Non-Uniform Memory Access). Es gibt eine Instanz des **Buffer Node** -Objekts für jeden verwendeten NUMA-Knoten. In einer Nicht-NUMA-Architektur gibt es eine einzelne Instanz des **Buffer Node** -Objekts.  
  
## <a name="buffer-node-performance-objects"></a>Leistungsobjekte für "Buffer Node"  
 In dieser Tabelle werden die Leistungsobjekte für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Node** beschrieben.  
  
|Buffer Node-Leistungsindikatoren von SQL Server|Description|  
|-------------------------------------|-----------------|  
|**Datenbankseiten**|Gibt die Anzahl der Seiten im Pufferpool auf diesem Knoten mit Datenbankinhalt an.|  
|**Lebenserwartung von Seiten**|Gibt die Mindestanzahl von Sekunden an, für die eine Seite ohne Verweise im Pufferpool auf diesem Knoten verbleibt.|  
|**Suchvorgänge in Seiten für lokalen Knoten/Sek.**|Gibt die Anzahl der Suchanforderungen von diesem Knoten an, die von diesem Knoten erfüllt wurden.|  
|**Suchvorgänge in Seiten für Remoteknoten/Sek.**|Gibt die Anzahl von Suchanforderungen von diesem Knoten an, die von anderen Knoten erfüllt wurden.|  
  
 Wenn SQL Server auf Nicht-NUMA-Hardware ausgeführt wird, sollten die Leistungsindikatoren der Objekte **Buffer Node** und **Puffer-Manager** übereinstimmen.  
  
 Auf NUMA-Hardware sollten die Summen der jeweiligen Leistungsindikatoren aller **Buffer Node** -Objekte ihren Gegenstücken von **Puffer-Manager**entsprechen.  
  
> [!NOTE]  
>  Die Werte und Summen der Leistungsindikatoren stimmen aufgrund der dynamischen Natur der Leistungsindikatoren und der Genauigkeit der Stichprobenahme möglicherweise nicht genau überein.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server, Puffer-Manager-Objekt](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
