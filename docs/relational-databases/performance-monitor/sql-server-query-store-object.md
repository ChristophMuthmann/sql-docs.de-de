---
title: SQL Server, Abfragespeicherobjekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 022f801293cb6ede334e0f4b70deceb37777b482
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-query-store-object"></a>SQL Server, Abfragespeicherobjekt
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Das Abfragespeicherobjekt enthält Leistungsindikatoren zum Überwachen der Ressourcenverwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Abfragetexten, Ausführungsplänen und Runtimestatistiken für Objekte wie z. B. gespeicherte Prozeduren, Ad-hoc- und vorbereitete [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und Trigger.  
  
 In dieser Tabelle werden die **SQLServer:Abfragespeicher**-Leistungsindikatoren beschrieben.  
  
|Leistungsindikatoren des SQL Server-Abfragespeichers|Beschreibung|  
|-------------------------------------|-----------------|  
|**CPU-Verwendung des Abfragespeichers**|Gibt die CPU-Nutzung durch Abfragespeicher an.|  
|**Logische Lesevorgänge des Abfragespeichers**|Gibt die Anzahl der logischen Lesevorgänge an, die durch den Abfragespeicher vorgenommen werden.|  
|**Logische Schreibvorgänge des Abfragespeichers**|Gibt an, wie viele Daten sich in der Warteschlange befinden, um aus dem Abfragespeicher geleert zu werden. Die Häufigkeit und Verzögerung beim Hinzufügen von Elementen zur Warteschlange (die Runtimestatistiken) werden durch die Einstellung für das Intervall für Datenleerung gesteuert.|  
|**Physische Lesevorgänge des Abfragespeichers**|Gibt die Anzahl der physischen Lesevorgänge an, die durch den Abfragespeicher vorgenommen werden.|  
  
 Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Abfragespeicherinstanz|Beschreibung|  
|--------------------------|-----------------|  
|**_Total**|Informationen für den Abfragespeicher für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|\<Name der Datenbank>|Abfragespeicherinformationen für diese Datenbank.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
