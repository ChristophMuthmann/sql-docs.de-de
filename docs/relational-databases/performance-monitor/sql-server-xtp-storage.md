---
title: "SQL Server-XTP-Speicher | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server-XTP-Speicher
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Das Leistungsobjekt „SQL Server-XTP-Speicher“ enthält Leistungsindikatoren, die sich auf die Speicherung auf Datenträger für In-Memory-OLTP in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beziehen.  
  
 In dieser Tabelle werden die Leistungsindikatoren von **SQL Server-XTP-Speicher** beschrieben.  
  
|Leistungsindikator|Beschreibung|  
|-------------|-----------------|  
|**Geschlossene Prüfpunkte**|Die Anzahl der vom Online-Agent geschlossenen Prüfpunkte.|  
|**Verarbeitete Prüfpunkte**|Die Anzahl der vom Offline-Prüfpunktthread verarbeiteten Prüfpunkte.|  
|**Abgeschlossene Kernzusammenführungen**|Die Anzahl der vom Zusammenführungsarbeitsthread abgeschlossenen Kernzusammenführungen. Diese Zusammenführungen müssen noch installiert werden.|  
|**Auswertungen der Zusammenführungsrichtlinie**|Die Anzahl der Auswertungen für die Zusammenführungsrichtlinie, seit der Server gestartet wurde.|  
|**Ausstehende Zusammenführungsanforderungen**|Die Anzahl der ausstehenden Zusammenführungsanforderungen, seit der Server gestartet wurde.|  
|**Abgebrochene Zusammenführungen**|Die Anzahl der aufgrund eines Fehlers abgebrochenen Zusammenführungen.|  
|**Installierte Zusammenführungen**|Die Anzahl der erfolgreich installierten Zusammenführungen.|  
|**Gesamtanzahl zusammengeführter Dateien**|Die Gesamtanzahl der zusammengeführten Quelldateien. Diese Anzahl kann verwendet werden, um die durchschnittliche Anzahl von Quelldateien in der Zusammenführung zu ermitteln.|  
  
## Siehe auch  
 [Leistungsindikatoren für SQL Server XTP &#40;In-Memory-OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  