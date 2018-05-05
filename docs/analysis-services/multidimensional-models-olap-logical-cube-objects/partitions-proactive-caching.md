---
title: Proaktives Zwischenspeichern (Partitionen) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e0368d82086013986d9cbed5c23362aa4976edab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="partitions---proactive-caching"></a>Partitionen - proaktives Zwischenspeichern
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Proaktives Zwischenspeichern ermöglicht automatische MOLAP-Cacheerstellung und die Verwaltung von OLAP-Objekten. Cubes integrieren auf der Grundlage der von der Datenbank empfangenen Benachrichtigungen unverzüglich die Änderungen, die an den Daten in der Datenbank vorgenommen wurden. Das Ziel der proaktiven Zwischenspeicherung ist die Bereitstellung der Leistung von herkömmlichem MOLAP, während die Unmittelbarkeit und die einfache Handhabung von ROLAP erhalten bleibt.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.ProactiveCaching>-Objekt besteht aus: Zeitsteuerungsspezifikation und Tabellenbenachrichtigung. Die Zeitsteuerungsspezifikation definiert den zeitlichen Rahmen zum Aktualisieren des Caches, nachdem eine Änderungsbenachrichtigung empfangen wurde. Die Tabellenbenachrichtigung definiert das Benachrichtigungsschema zwischen der Datentabelle und dem <xref:Microsoft.AnalysisServices.ProactiveCaching>-Objekt.  
  
 Die mehrdimensionale OLAP-Speicherung (MOLAP) bietet die besten Abfragereaktionen, allerdings mit dem Nachteil einer gewissen Latenzzeit für Daten. Bei der relationalen OLAP-Echtzeitspeicherung (ROLAP) können Benutzer die letzten Änderungen an einer Datenquelle sofort durchsuchen, allerdings mit dem Nachteil einer bedeutend schlechteren Leistung als bei der mehrdimensionalen OLAP (MOLAP), da keine im Voraus berechneten Datenzusammenfassungen vorhanden sind und die relationale Speicherung nicht für OLAP-Abfragen optimiert ist. Wenn Sie Anwendungen einsetzen, in denen Benutzer aktuelle Daten anzeigen müssen, und wenn Sie zudem die Leistungsvorteile der MOLAP-Speicherung nutzen möchten, bietet Ihnen SQL Server Analysis Services die Möglichkeit, diesen Anforderungen mit dem proaktiven Zwischenspeichern, insbesondere in Kombination mit der Verwendung von Partitionen, entgegenzukommen. Das proaktive Zwischenspeichern wird auf Partitions- und Dimensionsbasis festgelegt. Die Optionen für das proaktive Zwischenspeichern ermöglichen ein Gleichgewicht zwischen der verbesserten Leistung der MOLAP-Speicherung und der Unmittelbarkeit der ROLAP-Speicherung und bieten die automatische Partitionsverarbeitung basierend auf einem festgelegten Zeitplan oder bei Änderung der zugrunde liegenden Daten.  
  
## <a name="proactive-caching-configuration-options"></a>Konfigurationsoptionen für das proaktive Zwischenspeichern  
 SQL Server Analysis Services stellt mehrere Konfigurationsoptionen für das proaktive Zwischenspeichern bereit, mit denen Sie die Leistung maximieren, die Latenzzeit minimieren und die Verarbeitung planen können. Die Funktionen zum proaktiven Zwischenspeichern vereinfachen den Prozess der Verwaltung veralteter Daten. Die Einstellungen für das proaktive Zwischenspeichern bestimmen, wie oft die mehrdimensionale OLAP-Struktur, auch MOLAP-Cache genannt, neu erstellt wird, ob der veraltete MOLAP-Speicher beim Neuerstellen des Caches oder der zugrunde liegenden ROLAP-Datenquelle abgefragt wird und ob der Cache nach einem Zeitplan oder auf der Grundlage von Änderungen in der Datenbank neu erstellt wird.  
  
### <a name="minimizing-latency"></a>Minimieren der Latenzzeit  
 Wurde für das proaktive Zwischenspeichern festgelegt, dass die Latenzzeit minimiert wird, werden Benutzerabfragen für ein OLAP-Objekt entweder für die ROLAP-Speicherung oder die MOLAP-Speicherung ausgeführt, je nachdem, ob vor kurzer Zeit Änderungen an den Daten vorgenommen wurden und wie die proaktive Zwischenspeicherung konfiguriert ist. Die Abfrage-Engine leitet Abfragen an Quelldaten in der MOLAP-Speicherung, bis es zu Änderungen in der Datenquelle kommt. Zum Minimieren der Latenzzeit können nach dem Auftreten von Änderungen in einer Datenquelle zwischengespeicherte MOLAP-Objekte gelöscht werden, und die Abfrage kann zur ROLAP-Speicherung wechseln, während die MOLAP-Objekte im Cache neu erstellt werden. Nach dem Neuerstellen und Verarbeiten der MOLAP-Objekte wechseln Abfragen automatisch wieder zur MOLAP-Speicherung. Die Cacheaktualisierung kann bei einer kleinen Partition, z. B. der aktuellen Partition, die einen so kleinen Zeitraum wie den aktuellen Tag umfassen kann, äußerst schnell erfolgen.  
  
### <a name="maximizing-performance"></a>Maximieren der Leistung  
 Wenn Sie die Leistung maximieren und gleichzeitig die Latenzzeit reduzieren möchten, kann die Zwischenspeicherung auch ohne Löschen der aktuellen MOLAP-Objekte verwendet werden. Abfragen werden dann weiterhin für MOLAP-Objekte ausgeführt, während Daten in einen neuen Cache gelesen und dort verarbeitet werden. Diese Methode bietet eine bessere Leistung, kann jedoch dazu führen, dass Abfragen während des Erstellens des neuen Caches alte Daten zurückgeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Speichern von Dimensionen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Festlegen der Partitionsspeicher & #40; Analysis Services – mehrdimensional & #41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)  
  
  
