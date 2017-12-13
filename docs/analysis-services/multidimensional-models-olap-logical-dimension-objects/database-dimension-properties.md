---
title: Dimension Properties-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f22fa80ab461872b097ecd62eb54de1a22416c3c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="database-dimension-properties"></a>Eigenschaften von Datenbankdimensionen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], die Merkmale einer Dimension werden definiert, indem die Metadaten für die Dimension basierend auf den Einstellungen der verschiedenen Dimensionseigenschaften und auf die Attribute oder Hierarchien, die von der Dimension enthalten sind. In der folgenden Tabelle werden die Dimensionseigenschaften in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AttributeAllMemberName**|Gibt den Namen des Alle-Elements für Attribute in einer Dimension an.|  
|**Sortierung**|Bestimmt die von der Dimension verwendete Sortierung.|  
|**CurrentStorageMode**|Enthält den aktuellen Speichermodus für die Dimension.|  
|**' DependsOnDimension '**|Enthält die ID einer anderen Dimension, von der die Dimension abhängt, falls vorhanden.|  
|**Description**|Enthält die Beschreibung einer Dimension.|  
|**ErrorConfiguration**|Konfigurierbare Fehlerbehandlungseinstellungen für die Bearbeitung doppelter Schlüssel, unbekannter Schlüssel, für Fehlergrenzen, Aktionen bei Erkennung von Fehlern, Fehlerprotokolldateien und die Bearbeitung von NULL-Schlüsseln.|  
|**ID**|Enthält den eindeutigen Bezeichner (ID) der Dimension.|  
|**Sprache**|Gibt die Standardsprache für die Dimension an.|  
|**MdxMissingMemberMode**|Legt die Verarbeitung fehlender Elemente in MDX-Anweisungen (Multidimensional Expressions) fest.|  
|**MiningModelID**|Enthält die ID des Miningmodells, der die Data Mining-Dimension zugeordnet ist. Diese Eigenschaft kann nur angewendet werden, wenn die Dimension eine Miningmodelldimension ist.|  
|**Name**|Gibt den Namen der Dimension an.|  
|**ProactiveCaching**|Definiert die Einstellungen für die Dimension für die proaktive Zwischenspeicherung.|  
|**ProcessingGroup**|Gibt die Verarbeitungsgruppe an. Die Werte sind ByAttribute oder ByTable. Standardmäßig wird **ByAttribute**.|  
|**ProcessingMode**|Gibt an, ob [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] während oder nach der Verarbeitung indizieren und aggregieren soll.|  
|**ProcessingPriority**|Bestimmt die Verarbeitungspriorität der Dimension während Hintergrundvorgängen wie verzögerte Aggregation, Indizierung oder Clustererstellung.|  
|**Quelle**|Identifiziert die Datenquellensicht, an die die Dimension gebunden ist.|  
|**StorageMode**|Bestimmt den Speichermodus für die Dimension.|  
|**Typ**|Gibt den Typ der Dimension an.|  
|**UnknownMember**|Gibt an, ob das unbekannte Element sichtbar ist.|  
|**UnknownMemberName**|Gibt die Beschriftung in der standardmäßigen Sprache der Dimension für das unbekannte Element der Dimension an.|  
|**WriteEnabled**|Gibt an, ob das Rückschreiben von Dimensionen unterstützt wird (unterliegt den Sicherheitsberechtigungen).|  
  
> [!NOTE]  
>  Weitere Informationen zum Festlegen von Werten für die Eigenschaften ErrorConfiguration und UnknownMember bei der Arbeit mit null-Werte und anderen Problemen mit der Datenintegrität finden Sie unter [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Dimensionsbeziehungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
