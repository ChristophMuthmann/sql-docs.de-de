---
title: "SQL Server, Statistiken zu Batchantworten (Objekt) | Microsoft Docs"
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
  - "SQLServer:Statistiken zu Batchantworten"
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
caps.latest.revision: 3
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 3
---
# SQL Server, Statistiken zu Batchantworten (Objekt)
Das Leistungsobjekt **SQLServer:Statistiken zu Batchantworten** stellt Leistungsindikatoren zum Nachverfolgen von SQL Server-Batchantwortzeiten bereit.

In der folgenden Tabelle werden die SQL Server-Leistungsobjekte für **Statistiken zu Batchantworten** beschrieben.


|**SQL Server – Statistiken zu Batchantworten (Leistungsindikatoren)**|Description|  
|-------------|-----------------|  
|**Batches >= 000000 ms und \< 000001 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 0 ms, aber kleiner als 1 ms.|
|**Batches >= 000001 ms und \< 000002 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 1 ms, aber kleiner als 2 ms.|
|**Batches >= 000002 ms und \< 000005 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 2 ms, aber kleiner als 5 ms.|
|**Batches >= 000005 ms und \< 000010 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 5 ms, aber kleiner als 10 ms.|
|**Batches >= 000010 ms und \< 000020 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 10 ms, aber kleiner als 20 ms.|
|**Batches >= 000020 ms und \< 000050 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 20 ms, aber kleiner als 50 ms.|
|**Batches >= 000050 ms und \< 000100 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 50 ms, aber kleiner als 100 ms.|
|**Batches >= 000100 ms und \< 000200 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 100 ms, aber kleiner als 200 ms.|
|**Batches >= 000200 ms und \< 000500 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 200 ms, aber kleiner als 500 ms.|
|**Batches >= 000500 ms und \< 001000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 500 ms, aber kleiner als 1.000 ms.|
|**Batches >= 001000 ms und \< 002000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 1.000 ms, aber kleiner als 2.000 ms.|
|**Batches >= 002000 ms und \< 005000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 2.000 ms, aber kleiner als 5.000 ms.|
|**Batches >= 005000 ms und \< 010000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 5.000 ms, aber kleiner als 10.000 ms.|
|**Batches >= 010000 ms und \< 020000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 10.000 ms, aber kleiner als 20.000 ms.|
|**Batches >= 020000 ms und \< 050000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 20.000 ms, aber kleiner als 50.000 ms.|
|**Batches >= 050000 ms und \< 100000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 50.000 ms, aber kleiner als 100.000 ms.| 
|**Batches >= 100000 ms**|Die Anzahl der SQL-Batches mit einer Antwortzeit größer oder gleich 100.000 ms.| 

Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Element|Description|  
|----------|-----------------|  
|**CPU-Zeit: Anforderungen**|Die von der CPU für die Anforderung erforderliche Zeit.|  
|**CPU-Zeit: Gesamt(ms)**|Die von der CPU für den Batch erforderliche Gesamtzeit.|  
|**Verstrichene Zeit: Anforderungen**|Die für die Anforderung verstrichene Zeit.|  
|**Verstrichene Zeit: Gesamt(ms)**|Die für den Batch verstrichene Zeit.|  

## Siehe auch
[SQL Server, Plancache-Objekt](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[Überwachen der Ressourcenverwendung (Systemmonitor)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  