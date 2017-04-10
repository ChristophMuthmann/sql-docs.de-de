---
title: "Bew&#228;hrte Methoden f&#252;r zeitbasierte Zeilenfilter | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Bewährte Methoden"
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Bew&#228;hrte Methoden f&#252;r zeitbasierte Zeilenfilter
  Benutzer von Anwendungen benötigen häufig eine zeitbasierte Teilmenge der Daten in einer Tabelle. Ein Verkäufer könnte z. B. Daten zu Bestellungen der letzten Woche benötigen und ein Ereignisplaner Daten zu Ereignissen in der kommenden Woche. In vielen Fällen verwenden Clientanwendungen Abfragen, die die **GETDATE()** Funktion, um dies zu erreichen. Betrachten Sie die folgende Zeilenfilteranweisung:  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 Bei einem Filter dieses Typs wird davon ausgegangen, dass zwei Aktionen eingeleitet werden, wenn der Merge-Agent ausgeführt wird: Zeilen, die dem Filter entsprechen, werden auf die Abonnenten repliziert, und für Zeilen, die dem Filter nicht mehr entsprechen, wird auf den Abonnenten ein Cleanup ausgeführt. (Weitere Informationen zum Filtern mit **HOST_NAME()**, finden Sie unter [parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md).) Die Replikation und das Cleanup werden bei einer Mergereplikation jedoch nur für Daten durchgeführt, die seit der letzten Synchronisierung geändert wurden, unabhängig davon, wie ein Zeilenfilter für diese Daten definiert wurde.  
  
 Damit eine Zeile bei der Mergereplikation verarbeitet wird, müssen die Daten in der Zeile dem Zeilenfilter entsprechen, und sie müssen seit der letzten Synchronisierung geändert worden sein. In der **SalesOrderHeader** -Tabelle wird **OrderDate** eingegeben, wenn eine Zeile eingefügt wird. Die Zeilen werden wie erwartet auf den Abonnenten repliziert, da die Einfügung eine Datenänderung darstellt. Befinden sich auf dem Abonnenten jedoch Zeilen, die dem Filter nicht mehr entsprechen (z. B. für Bestellungen, die mehr als sieben Tage zurückliegen), werden sie vom Abonnenten nicht entfernt, es sei denn, sie wurden aus einem anderen Grund aktualisiert.  
  
 Das Beispiel des Ereignisplaners veranschaulicht das Problem mit dieser Art der Filterung. Betrachten Sie den folgenden Filter für eine **Events** -Tabelle:  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 In einer Tabelle mit Ereignissen erfolgen Einfügungen möglicherweise vor dem Datum des Ereignisses. Wenn die Einfügung für ein Ereignis in der kommenden Woche bereits vor einem Monat erfolgt ist und die Zeile nicht aus einem anderen Grund aktualisiert wurde, wird die Zeile auf dem Abonnenten nicht repliziert, auch dann nicht, wenn sie dem Zeilenfilter entspricht.  
  
 Abhängig von der Konfiguration der Veröffentlichung wertet die Mergereplikation Filter außerdem zu unterschiedlichen Zeiten aus:  
  
-   Verwendet eine Veröffentlichung vorausberechnete Partitionen (Standardeinstellung), werden die Filter beim Einfügen oder Aktualisieren einer Zeile ausgewertet.  
  
-   Verwendet die Veröffentlichung keine vorausberechneten Partitionen, werden die Filter beim Ausführen des Merge-Agents ausgewertet.  
  
 Weitere Informationen zu vorausberechneten Partitionen finden Sie unter [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Der Zeitpunkt der Auswertung des Filters wirkt sich darauf aus, welche Daten den Filter erfüllen. Wenn eine Veröffentlichung z. B. vorausberechnete Partitionen verwendet und Sie die Daten alle zwei Tage synchronisieren, könnte die Teilmenge der Daten für den Verkäufer Zeilen enthalten, die bis zu zwei Tage älter sind als erwartet.  
  
## Empfehlungen für die Verwendung zeitbasierter Zeilenfilter  
 Die folgende Methode stellt einen leistungsfähigen und unkomplizierten Ansatz für die zeitbasierte Filterung bereit:  
  
-   Fügen Sie der Tabelle eine Spalte des **bit**-Datentyps hinzu. Diese Spalte gibt an, ob eine Zeile repliziert werden soll.  
  
-   Verwenden Sie einen Zeilenfilter, der auf die neue Spalte und nicht auf eine zeitbasierte Spalte verweist.  
  
-   Erstellen Sie einen SQL Server-Agent-Auftrag (oder einen Auftrag, der mithilfe eines anderen Mechanismus geplant wurde), der die Spalte vor der geplanten Ausführung des Merge-Agents aktualisiert.  
  
 Dieser Ansatz die Mängel bei der Verwendung von **GETDATE()** oder einer anderen zeitbasierten Methode und vermeidet das Problem zu bestimmen, wann Filter für Partitionen ausgewertet werden. Betrachten Sie das folgende Beispiel einer **Events** -Tabelle:  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replizieren**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|1|  
|2|Dinner|112|2006-10-10|0|  
|3|Party|112|2006-10-11|0|  
|4|Wedding|112|2006-10-12|0|  
  
 Der Zeilenfilter für diese Tabelle würde dann folgendermaßen aussehen:  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 Der SQL Server-Agent-Auftrag könnte vor jeder Ausführung des Merge-Agents [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Anweisungen wie die folgenden ausführen:  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 Die erste Zeile setzt die **Replicate** -Spalte auf **0**zurück, und die zweite Zeile setzt die Spalte für Ereignisse, die in den nächsten sieben Tagen stattfinden, auf **1** . Wenn diese [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung am 07.10.2006 ausgeführt wird, wird die Tabelle folgendermaßen aktualisiert:  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replizieren**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|0|  
|2|Dinner|112|2006-10-10|1|  
|3|Party|112|2006-10-11|1|  
|4|Wedding|112|2006-10-12|1|  
  
 Die Ereignisse für die nächste Woche sind nunmehr als replikationsbereit markiert. Wird der Merge-Agent das nächste Mal für das Abonnement ausgeführt, das der Ereigniskoordinator 112 verwendet, werden die Zeilen 2, 3 und 4 auf den Abonnenten heruntergeladen, und die Zeile 1 wird vom Abonnenten entfernt.  
  
## Siehe auch  
 [GETDATE & #40; Transact-SQL & #41;](../../../t-sql/functions/getdate-transact-sql.md)   
 [Implementieren von Aufträgen](../../../ssms/agent/implement-jobs.md)   
 [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  