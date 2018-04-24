---
title: SQL Server, 'Statistiken für Ressourcenpools'-Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
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
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24853ad0bfcd473c7f67492f187292118b639f55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server, 'Statistiken für Ressourcenpools'-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das SQLServer:Statistiken für Ressourcenpools-Objekt enthält Leistungsindikatoren, die Informationen zur Ressourcenkontrollen-Poolstatistik zurückgeben.  
  
 Jeder aktive Ressourcenpool erstellt eine Instanz des Leistungsobjekts SQLServer:Statistiken für Ressourcenpools, wobei der Name der Instanz dem Namen des Ressourcenpools in der Ressourcenkontrolle entspricht. In der folgenden Tabelle sind die für diese Instanz unterstützten Leistungsindikatoren beschrieben.  
  
|Indikatorname|Description|  
|------------------|-----------------|  
|**Menge aktiver Arbeitsspeicherzuweisungen (KB)**|Der aktuell zugewiesene Gesamtspeichers in Kilobyte (KB). Diese Information ist auch in [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)verfügbar.| 
|**Anzahl aktiver Arbeitsspeicherzuweisungen**|Die aktuelle Gesamtanzahl von Arbeitsspeicherzuweisungen. Diese Information ist auch in [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)verfügbar.|  
|**Durchschnittl. Datenträgerzeit (ms)**|Die durchschnittliche Zeit (in Millisekunden) eines Lesevorgangs vom Datenträger.|  
|**Basis für durchschnittl. Datenträgerzeit (ms)**|Nur zur internen Verwendung.|
|**Durchschnittl. Datenträgerzeit (ms)/Schreiben E/A**|Die durchschnittliche Zeit (in Millisekunden) eines Schreibvorgangs auf den Datenträger.|  
|**Basis für Datenträgerzeit (ms)/Schreiben E/A**|Nur zur internen Verwendung.|
|**Cachespeicherziel (KB)**|Das aktuelle Speicherbrokerziel für den Cache in Kilobyte (KB).|  
|**Speicherziel für Kompilierung (KB)**|Das aktuelle Speicherbrokerziel für Abfragekompilierungen in Kilobyte (KB).|  
|**Auswirkungen der CPU-Kontrolle in %**|Die Auswirkungen der Ressourcenkontrolle auf den Ressourcenpool. Wird wie folgt berechnet: (CPU-Verwendung in %) / (CPU-Verwendung in % ohne Ressourcenkontrolle).|  
|**CPU verzögert %**|System-CPU verzögert für alle Anforderungen in der angegebenen Instanz des Leistungsobjekts als Prozentsatz der gesamten aktiven Zeit.|
|**Basis für CPU verzögert %**|Nur zur internen Verwendung.|
|**CPU effektiv %**|System-CPU-Verwendung für alle Anforderungen in der angegebenen Instanz des Leistungsobjekts als Prozentsatz der gesamten aktiven Zeit.|
|**Basis für CPU effektiv %**|Nur zur internen Verwendung.|
|**CPU-Verwendung in %**|Die von allen Anforderungen in allen Arbeitsauslastungsgruppen dieses Pools belegte CPU-Bandbreite. Dieser Wert wird relativ zum Computer gemessen und auf alle CPUs im System normalisiert. Dieser Wert ändert sich, wenn sich die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess verfügbare CPU-Leistung ändert. Der Wert wird auf die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess empfangenen Elemente normalisiert.|  
|**Basis für CPU-Verwendung in %**|Nur zur internen Verwendung.|
|**Ziel-CPU-Verwendung in %**|Der Zielwert für die CPU-Auslastung in Prozent für den Ressourcenpool. Dieser Wert basiert auf den Konfigurationseinstellungen für den Ressourcenpool und der Systemauslastung.|  
|**CPU-Verletzung %**|Der Unterschied zwischen der CPU-Reservierung und dem effektiv für Zeitplanung aufgewendeten Prozentsatz.|
|**Vom Datenträger gelesene Bytes/s**|Die Anzahl der in der letzten Sekunde vom Datenträger gelesenen Bytes.|  
|**Gedrosselte E/A-Lesevorgänge auf Datenträger/s**|Die Anzahl der in der letzten Sekunde gedrosselten Lesevorgänge.|  
|**E/A-Lesevorgänge von Datenträger/s**|Die Anzahl der Lesevorgänge vom Datenträger in der letzten Sekunde.| 
|**Auf den Datenträger geschriebene Bytes/s**|Die Anzahl der in der letzten Sekunde auf den Datenträger geschriebenen Bytes.|  
|**Gedrosselte E/A-Schreibvorgänge auf Datenträger/s**|Die Anzahl der in der letzten Sekunde gedrosselten Schreibvorgänge.| 
|**E/A-Schreibvorgänge auf Datenträger/s**|Die Anzahl der Schreibvorgänge auf den Datenträger in der letzten Sekunde.|
|**Maximaler Arbeitsspeicher (KB)**|Die maximale Menge an Arbeitsspeicher in Kilobyte (KB), die der Ressourcenpool basierend auf den Einstellungen für den Ressourcenpool und dem Serverstatus aufweisen kann.| 
|**Timeouts für Arbeitsspeicherzuweisungen/Sekunde**|Die Anzahl von Timeouts für Arbeitsspeicherzuweisungen pro Sekunde.|
|**Arbeitsspeicherzuweisungen/Sekunde**|Die Anzahl von Arbeitsspeicherzuweisungen, die pro Sekunde in diesem Ressourcenpool ausgeführt werden.| 
|**Anzahl ausstehender Arbeitsspeicherzuweisungen**|Die Anzahl von Anforderungen in der Warteschlange, die auf Arbeitsspeicherzuweisungen warten. Diese Information ist auch in [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)verfügbar.|
|**Speicherziel für Abfrageausführung (KB)**|Das aktuelle Speicherbrokerziel für die Arbeitsspeicherzuweisung der Abfrageausführung in Kilobyte (KB). Diese Information ist auch in [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)verfügbar.|  
|**Zielspeicher (KB)**|Der Zielarbeitsspeicher in Kilobyte (KB), die der Ressourcenpool, auf Grundlage der Einstellungen für den Ressourcenpool und des Serverstatus, abzurufen versucht.|   
|**Verwendeter Arbeitsspeicher (KB)**|Die im Ressourcenpool verwendete Arbeitsspeichermenge in Kilobyte (KB).|  

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, 'Statistiken für Arbeitsauslastungsgruppen'-Objekt](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)  
  
  
