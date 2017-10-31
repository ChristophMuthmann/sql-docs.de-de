---
title: MSSQLSERVER_32044 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 55a88fbb8340cba70ae47316461758c2a172b2fd
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver32044"></a>MSSQLSERVER_32044
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|32044|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLErrorNum32044|  
|Meldungstext|Die Warnung für 'Spiegelungscommitaufwand' wurde ausgelöst. Der aktuelle Wert von '%d' überschreitet den Threshold '%d'.|  
  
## <a name="explanation"></a>Erklärung  
Dieses Datenbankspiegelungsereignis wird auf der Prinzipalserverinstanz ausgegeben. Damit soll angegeben werden, dass aufgrund der Datenbankspiegelung mit der gesamten Wartezeit für den Commit ein vom Benutzer angegebener Schwellenwert erreicht oder überschritten wurde. Die Wartezeit ist das Produkt der Anzahl von Transaktionen und der jeweiligen Dauer. Beispielsweise entstehen in den folgenden zwei Fällen jeweils 1000 Millisekunden Wartezeit: 1000 Transaktionen * 1 Millisekunde und 1 Transaktion \* 1000 Millisekunden. Eine erhöhte Commitwartezeit kann durch einen starken Anstieg der Anzahl von Transaktionen, durch Verzögerungen beim Senden des Protokolls oder Verzögerungen beim Leeren des Protokolls auf der Spiegelserverinstanz verursacht werden.  
  
Der Spiegelungscommitaufwand ist eine Leistungsmetrik, mit der Sie die aktuelle Leistungsauswirkung des synchronen Vorgangs beurteilen können. Diese Metrik ist nur im Modus für hohe Sicherheit relevant. Da der Modus für hohe Sicherheit synchron ausgeführt wird, wartet die Prinzipalserverinstanz darauf, einen Commit für die Transaktion auszuführen, nachdem ein Protokolldatensatz an die Spiegelserverinstanz gesendet wurde, bis eine Bestätigung darüber eingeht, dass der Protokolldatensatz von der Spiegelserverinstanz auf einen Datenträger geschrieben wurde. Der Protokolldatensatz verbleibt auf dem Datenträger der Spiegelserverinstanz, solange auf die Wiederherstellung in der Spiegeldatenbank gewartet wird.  
  
## <a name="user-action"></a>Benutzeraktion  
Prüfen Sie die Auslastung für die Instanzen des Prinzipalservers und des Spiegelservers sowie die entsprechenden Netzwerkverbindungen, um die Ursache zu ermitteln.  
  
## <a name="see-also"></a>Siehe auch  
[Datenbankspiegelung &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[Verwenden von Warnungsschwellenwerten und Warnmeldungen für Spiegelungsleistungsmetriken &#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  

