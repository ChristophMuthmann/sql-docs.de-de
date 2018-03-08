---
title: SQL Server-XTP-Speicher | Microsoft-Dokumentation
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
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: "6"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2bb4803233db54eea8d3acfb5cb5e2284cc606fb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-xtp-storage"></a>SQL Server-XTP-Speicher
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das Leistungsobjekt „SQL Server-XTP-Speicher“ enthält Leistungsindikatoren, die sich auf die Speicherung auf Datenträger für In-Memory-OLTP in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]beziehen.  
  
 In dieser Tabelle werden die Leistungsindikatoren von **SQL Server-XTP-Speicher** beschrieben.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|**Geschlossene Prüfpunkte**|Die Anzahl der vom Online-Agent geschlossenen Prüfpunkte.|  
|**Verarbeitete Prüfpunkte**|Die Anzahl der vom Offline-Prüfpunktthread verarbeiteten Prüfpunkte.|  
|**Abgeschlossene Kernzusammenführungen**|Die Anzahl der vom Zusammenführungsarbeitsthread abgeschlossenen Kernzusammenführungen. Diese Zusammenführungen müssen noch installiert werden.|  
|**Auswertungen der Zusammenführungsrichtlinie**|Die Anzahl der Auswertungen für die Zusammenführungsrichtlinie, seit der Server gestartet wurde.|  
|**Ausstehende Zusammenführungsanforderungen**|Die Anzahl der ausstehenden Zusammenführungsanforderungen, seit der Server gestartet wurde.|  
|**Abgebrochene Zusammenführungen**|Die Anzahl der aufgrund eines Fehlers abgebrochenen Zusammenführungen.|  
|**Installierte Zusammenführungen**|Die Anzahl der erfolgreich installierten Zusammenführungen.|  
|**Gesamtanzahl zusammengeführter Dateien**|Die Gesamtanzahl der zusammengeführten Quelldateien. Diese Anzahl kann verwendet werden, um die durchschnittliche Anzahl von Quelldateien in der Zusammenführung zu ermitteln.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
