---
title: Cubeeigenschaften - mehrdimensionalen Modell Programmierung | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7dd5d6a976c21b7413b24ba59310cdd95c6fd13e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cube-properties---multidimensional-model-programming"></a>Cubeeigenschaften - mehrdimensionalen Modell Programmierung
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cubes verfügen über eine Reihe von Eigenschaften, die Sie festlegen können und die sich auf das cubeweite Verhalten auswirken. Diese Eigenschaften sind in der folgenden Tabelle zusammengefasst.  
  
> [!NOTE]  
>  Manche Eigenschaften werden beim Erstellen des Cubes automatisch festgelegt und können nicht geändert werden.  
  
 Weitere Informationen zum Festlegen von Cubeeigenschaften finden Sie unter [Cubeentwickler &#40;Analysis Services – mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/a6692467-da88-4312-8b03-d812f2ae5a96).  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AggregationPrefix**|Gibt das für Aggregationsnamen verwendete gemeinsame Präfix an.|  
|**Sortierung**|Gibt den Gebietsschemabezeichner (LCID) und das Vergleichsflag, durch einen Unterstrich voneinander getrennt, an, wie z. B. Latin1_General_C1_AS.|  
|**DefaultMeasure**|Enthält einen mehrdimensionalen Ausdruck (Multidimensional Expression, MDX), der das Standardmeasure für den Cube definiert.|  
|**Beschreibung**|Stellt eine Beschreibung des Cubes bereit, die in Clientanwendungen verwendet werden kann.|  
|**ErrorConfiguration**|Enthält konfigurierbare Fehlerbehandlungseinstellungen für die Bearbeitung doppelter Schlüssel, unbekannter Schlüssel, für Fehlergrenzen, Aktionen bei Erkennung von Fehlern, Fehlerprotokolldateien und die Bearbeitung von NULL-Schlüsseln.|  
|**EstimatedRows**|Gibt die Anzahl der geschätzten Zeilen im Cube an.|  
|**ID**|Enthält den eindeutigen Bezeichner (ID) des Cubes.|  
|**Sprache**|Gibt den Standardsprachbezeichner für den Cube an.|  
|**Name**|Gibt den benutzerfreundlichen Namen des Attributs an.|  
|**ProactiveCaching**|Definiert die Einstellungen für den Cube für die proaktive Zwischenspeicherung.|  
|**ProcessingMode**|Gibt an, ob während oder nach der Verarbeitung indiziert und aggregiert werden soll. Optionen sind **reguläre** oder **lazy**.|  
|**ProcessingPriority**|Legt die Verarbeitungspriorität des Cubes bei Hintergrundvorgängen wie z. B. verzögerte Aggregationen und Indizierungen fest. Der Standardwert ist **0**.|  
|**ScriptCacheProcessingMode**|Gibt an, ob der Skriptcache während oder nach der Verarbeitung erstellt werden soll. Optionen sind **reguläre** und **lazy**.|  
|**ScriptErrorHandlingMode**|Bestimmt die Fehlerbehandlung. Optionen sind **' ignorenone '** oder **' ignoreall '**|  
|**Quelle**|Zeigt die für den Cube verwendete Datenquellensicht.|  
|**StorageLocation**|Gibt den Speicherort des Dateisystems für den Cube an. Wenn kein Speicherort angegeben ist, wird er von der Datenbank geerbt, die das Cubeobjekt enthält.|  
|**StorageMode**|Gibt den Speichermodus für den Cube an. Werte sind **MOLAP**, **ROLAP**, oder **HOLAP**.|  
|**Visible**|Bestimmt die Sichtbarkeit des Cubes.|  
  
> [!NOTE]  
>  Weitere Informationen zum Festlegen von Werten für die ErrorConfiguration-Eigenschaft, bei der Arbeit mit null-Werte und anderen Problemen mit der Datenintegrität finden Sie unter [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Siehe auch  
 [Proaktives Zwischenspeichern & #40; Partitionen & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)  
  
  
