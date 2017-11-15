---
title: SQL Server, Sperren-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Locks object
- SQLServer:Locks
ms.assetid: ace04f0d-3993-4444-8317-ca39d7087e49
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d9a60e5e072a0c6b5d9d769aa07b57a921f678c7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-locks-object"></a>SQL Server, Sperren-Objekt
  Das **SQLServer:Locks** -Objekt in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sperren für einzelne Ressourcentypen zur Verfügung. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcen, wie etwa Zeilen, die während einer Transaktion gelesen oder geändert werden, werden mit Sperren belegt, um die zeitgleiche Verwendung der Ressourcen durch verschiedene Transaktionen zu verhindern. Wenn beispielsweise eine Zeile in einer Tabelle von einer Transaktion mit einer exklusiven Sperre (X) belegt wird, kann diese Zeile erst dann von einer anderen Transaktion geändert werden, wenn die Sperre aufgehoben wird. Durch die Reduzierung der Anzahl von Sperren kann die Parallelität erhöht werden, wodurch sich die Leistung verbessert. Es können mehrere Instanzen des **Sperren** -Objekts gleichzeitig überwacht werden, wobei jede Instanz eine Sperre für einen Ressourcentyp darstellt.  
  
 In dieser Tabelle werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Sperren** beschrieben.  
  
|Sperren-Leistungsindikatoren von SQL Server|Beschreibung|  
|-------------------------------|-----------------|  
|**Durchschnittliche Wartezeit (ms)**|Die durchschnittliche Länge der Wartezeit (in Millisekunden) für jede Sperranforderung, die nicht sofort erfüllt werden konnte.|  
|**Basis für durchschnittliche Wartezeit**|Nur zur internen Verwendung.|
|**Sperranforderungen/Sekunde**|Anzahl von neuen Sperren und Sperrkonvertierungen pro Sekunde, die vom Sperren-Manager angefordert wurden.|  
|**Sperrtimeouts/Sekunde (Timeout > 0)**|Die Anzahl von Sperranforderungen pro Sekunde, für die ein Timeout eingetreten ist. Interne Anforderungen für NOWAIT-Sperren sind darin nicht eingeschlossen.|  
|**Sperrtimeouts/Sekunde**|Die Anzahl von Sperranforderungen pro Sekunde, für die ein Timeout eingetreten ist. Dies umfasst auch Anforderungen für NOWAIT-Sperren.|  
|**Wartezeit für Sperre (ms)**|Gesamtwartezeit (in Millisekunden) für Sperren in der vergangenen Sekunde.|  
|**Sperrenwartevorgänge/Sekunde**|Anzahl von Sperranforderungen pro Sekunde, bei denen der aufrufende Prozess warten musste.|  
|**Anzahl von Deadlocks/Sekunde**|Anzahl von Sperranforderungen pro Sekunde, die zu einem Deadlock geführt haben.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann die folgenden Ressourcen sperren.  
  
|Element|Beschreibung|  
|----------|-----------------|  
|**_Total**|Informationen für alle Sperren.|  
|**AllocUnit**|Eine Sperre für eine Zuweisungseinheit.|  
|**Application**|Eine Sperre für eine anwendungsspezifische Ressource.|  
|**Datenbank**|Eine Sperre für eine Datenbank, einschließlich aller Objekte in der Datenbank.|  
|**Extent**|Eine Sperre für eine zusammenhängende Gruppe von 8 Seiten.|  
|**File**|Eine Sperre für eine Datenbankdatei.|  
|**Heap/BTree**|Heap oder BTree (HOBT). Eine Sperre für einen Heap von Datenseiten oder für die BTree-Struktur eines Indexes.|  
|**Key**|Eine Sperre für eine Zeile in einem Index.|  
|**Metadaten**|Eine Sperre für eine Kataloginformationskomponente, die auch als Metadaten bezeichnet wird.|  
|**Objekt**|Eine Sperre für eine Tabelle, gespeicherte Prozedur, Sicht usw., einschließlich aller Daten und Indizes. Hierbei kann es sich um ein beliebiges Objekt handeln, das einen Eintrag in **sys.all_objects**aufweist.|  
|**Page**|Eine Sperre für eine 8-KB-Seite in einer Datenbank.|  
|**RID**|Zeilen-ID. Eine Sperre für eine einzelne Zeile in einem Heap.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
