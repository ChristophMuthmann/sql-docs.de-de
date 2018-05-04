---
title: Konfigurieren von Measuregruppeneigenschaften | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5bb9a3be83529e2e195b1f6eaf375932949f253d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-measure-group-properties"></a>Konfigurieren von Measuregruppeneigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Measuregruppen haben Eigenschaften, die es Ihnen ermöglichen, die Funktionsweise von Measuregruppen zu definieren.  
  
## <a name="measure-group-properties"></a>Eigenschaften von Measuregruppen  
 Die Eigenschaften von Measuregruppen bestimmen das Verhalten innerhalb der gesamten Measuregruppe und legen das Standardverhalten für bestimmte Eigenschaften von Measures innerhalb einer Measuregruppe fest.  
  
|Eigenschaft|Definition|  
|--------------|----------------|  
|**AggregationPrefix**|Gilt für die ROLAP-Speicherung. Weist den indizierten Sichten in SQL Server ein gemeinsames Präfix zu, das zum Speichern von Aggregationen für die mit dieser Measuregruppe verknüpften Partitionen verwendet wird.|  
|**DataAggregation**|Diese Eigenschaft ist für die zukünftige Verwendung reserviert und hat derzeit keine Auswirkungen. Aus diesem Grund wird empfohlen, diese Einstellung nicht zu ändern.|  
|**Beschreibung**|Mit dieser Eigenschaft können Sie die Measuregruppe dokumentieren.|  
|**ErrorConfiguration**|Konfigurierbare Fehlerbehandlungseinstellungen für die Bearbeitung doppelter Schlüssel, unbekannter Schlüssel, für Fehlergrenzen, Aktionen bei Erkennung von Fehlern, Fehlerprotokolldateien und die Bearbeitung von NULL-Schlüsseln. Weitere Informationen finden Sie unter [Fehlerkonfiguration für die Verarbeitung von Cubes, Partitionen und Dimensionen &#40;SSAS - mehrdimensional&#41;](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md).|  
|**EstimatedRows**|Gibt die geschätzte Anzahl von Zeilen in der Faktentabelle an.|  
|**EstimatedSize**|Gibt die geschätzte Größe (in Byte) der Measuregruppe an.|  
|**ID**|Gibt den Bezeichner des Objekts an.|  
|**IgnoreUnrelatedDimensions**|Bestimmt, ob nicht verknüpfte Dimensionen auf ihre höchste Ebene gezwungen werden, wenn Elemente von Dimensionen, die nicht mit der Measuregruppe verknüpft sind, in eine Abfrage eingeschlossen werden. Die Standardeinstellung ist **True**.|  
|**Name**|Name des Measures. Diese Eigenschaft ist schreibgeschützt.|  
|**ProactiveCaching**|Konfigurierbare Fehlerbehandlungseinstellungen für die Bearbeitung doppelter Schlüssel, unbekannter Schlüssel, für Fehlergrenzen, Aktionen bei Erkennung von Fehlern, Fehlerprotokolldateien und die Bearbeitung von NULL-Schlüsseln.|  
|**ProcessingMode**|Gibt an, ob während oder nach der Verarbeitung indiziert und aggregiert werden soll. Die verfügbaren Optionen sind Regular und LazyAggregations. LazyAggregations kann verwendet werden, um die Aggregation als Hintergrundaufgabe auszuführen.|  
|**ProcessingPriority**|Legt die Verarbeitungspriorität des Cubes bei Hintergrundvorgängen wie z. B. verzögerte Aggregationen und Indizierungen fest. Der Standardwert ist **0**.|  
|**StorageLocation**|Der Speicherort des Dateisystems für die Measuregruppe. Wird kein Speicherort angegeben, wird er vom Cube geerbt, der die Measuregruppe enthält.|  
|**StorageMode**|Der Speichermodus für die Measuregruppe. Die verfügbaren Werte sind MOLAP, ROLAP und HOLAP.|  
|**Typ**|Gibt den Typ der Measuregruppe an.|  
  
  
