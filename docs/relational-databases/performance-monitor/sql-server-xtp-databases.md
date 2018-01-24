---
title: SQL Server XTP-Datenbanken | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQL Server 2016 XTP Databases
ms.assetid: 488ff55e-173f-43f6-9bdb-67b35e7cebfe
caps.latest.revision: "3"
author: dagiro
ms.author: v-dagir
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa4b8d6262311f68e0833366c4f0f2c5b6d71c53
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-xtp-databases"></a>SQL Server XTP-Datenbanken
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Das Leistungsobjekt **SQL Server XTP-Datenbanken** spezifische In-Memory-OLTP-Datenbanken bereit.

> [!NOTE]
>  Die SQL Server XTP-Datenbanken-Indikatoren sind aktuell in „sys.dm_os_performance_counters“ nicht sichtbar.  Die Indikatoren können im [System-Monitor](../../relational-databases/performance/start-system-monitor-windows.md)angezeigt werden.

Diese Tabelle beschreibt die **SQL Server XTP-Datenbanken** -Leistungsindikatoren.

|Leistungsindikator|Description| 
|-------------|-----------------|  
|**Durchschnittliches Transaktionssegment – großer Datenumfang**|Mittlere Größe von Transaktionssegmenten bei großer Datennutzlast. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**Durchschnittliche Transaktionssegmentgröße**|Mittlere Größe von Transaktionssegmenten der Nutzlast. Wenn dieser Wert gegen null tendiert, werden mehr Seiten aus der Back-End-Zuweisung zugewiesen. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**Thread leeren – 256K Warteschlangentiefe**|Tiefe der Threadbereinigungs-Warteschlange für E/A-Anforderungen mit 256K.|
|**Thread leeren – 4K Warteschlangentiefe**|Tiefe der Threadbereinigungs-Warteschlange für E/A-Anforderungen mit 4K.|
|**Thread leeren – 64K Warteschlangentiefe**|Tiefe der Threadbereinigungs-Warteschlange für E/A-Anforderungen mit 64K.|
|**Unveränderliche E/A-Threads/s leeren (256K)**|Die Anzahl der 256K-E/A-Anforderungen während der Verarbeitung der Seitenlöschung oberhalb der Sperrgrenze, die daher nicht ausgegeben werden können.|
|**Unveränderliche E/A-Threads/s leeren (4K)**|Die Anzahl der 4K-E/A-Anforderungen während der Verarbeitung der Seitenlöschung oberhalb der Sperrgrenze, die daher nicht ausgegeben werden können.|
|**Unveränderliche E/A-Threads/s leeren (64K)**|Die Anzahl der 64K-E/A-Anforderungen während der Verarbeitung der Seitenlöschung oberhalb der Sperrgrenze, die daher nicht ausgegeben werden können.|
|**IoPagePool256K kostenlose Listenanzahl**|Anzahl der Seiten in der Freiliste im 256K-E/A-Seitenpool. Wenn dieser Wert gegen null tendiert, werden mehr Seiten aus der Back-End-Zuweisung zugewiesen. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**IoPagePool256K insgesamt zugeordnet**|Gesamtzahl der dem 256K E/A-Seitenpool von der Back-End-Zuweisung zugewiesenen und gehaltenen Seiten. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**IoPagePool4K kostenlose Listenanzahl**|Anzahl der Seiten in der Freiliste des 4K-E-/A-Seitenpools. Wenn dieser Wert gegen null tendiert, werden mehr Seiten aus der Back-End-Zuweisung zugewiesen. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**IoPagePool4K insgesamt zugeordnet**|Gesamtzahl der dem 4K E/A-Seitenpool von der Back-End-Zuweisung zugewiesenen und gehaltenen Seiten. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**IoPagePool64K kostenlose Listenanzahl**|Anzahl der Seiten in der Freiliste im 64K-E/A-Seitenpool. Wenn dieser Wert gegen null tendiert, werden mehr Seiten aus der Back-End-Zuweisung zugewiesen. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**IoPagePool64K insgesamt zugeordnet**|Gesamtzahl der dem 64K E/A-Seitenpool von der Back-End-Zuweisung zugewiesenen und gehaltenen Seiten. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 256K-Erweiterungsanzahl**|Anzahl der Erweiterungen eines 256K-MtLogs. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 256K IOs ausstehend**|Die Anzahl der ausstehenden 256K E/A-Anforderungen, die von MtLog ausgegeben wurden.|
|**MtLog 256K Seitenfüllung %/Seite geleert**|Durchschnittlicher Füllprozentsatz jeder gelöschten 256K-MtLog-Seite. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 256K geschriebene Bytes/s**|Schreiben von Bytes pro Sekunde auf 256K MtLog-Objekte. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 4K-Erweiterungsanzahl**|Anzahl der Erweiterungen eines 4K-MtLogs. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 4K IOs ausstehend**|Die Anzahl der ausstehenden 4K E/A-Anforderungen, die von MtLog ausgegeben wurden.|
|**MtLog 4K Seitenfüllung %/Seite geleert**|Durchschnittlicher Füllprozentsatz jeder gelöschten 4K-MtLog-Seite. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 4K geschriebene Bytes/s**|Geschriebene Bytes pro Sekunde auf 4K MtLog-Objekte. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 64K Anzahl erweitern**|Anzahl der Erweiterungen eines 64K-MtLogs. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 64K IOs ausstehend**|Die Anzahl der ausstehenden 64K E/A-Anforderungen, die von MtLog ausgegeben wurden.|
|**MtLog 64K Seitenfüllung %/Seite geleert**|Durchschnittlicher Füllprozentsatz jeder gelöschten 64K-MtLog-Seite. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**MtLog 64K geschriebene Bytes/s**|Geschriebene Bytes pro Sekunde auf 64K MtLog-Objekte. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**Mergeanzahl**|Anzahl der aktiven Merges.|
|**Mergeanzahl/s**|Die Anzahl der pro Sekunde erstellten Merges (im Mittel).|
|**Anzahl Serialisierungen**|Die Anzahl der aktiven Serialisierungen.|
|**Anzahl Serialisierungen/s**|Die Anzahl der pro Sekunde erstellten Serialisierungen (im Mittel)).|
|**Seitenanzahl für Endsegmentcache**|Anzahl der im Endsegmentcache zugeordneten Seiten. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|
|**Spitzenwert der Seitenanzahl im Endsegmentcache**|Größte Anzahl Seiten, die im Endsegmentcache zugewiesen wurden. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|


## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
