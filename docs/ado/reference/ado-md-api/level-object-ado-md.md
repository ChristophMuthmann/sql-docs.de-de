---
title: Level-Objekt (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02a1a7e433c13c52db6c1e9112437470769c76be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="level-object-ado-md"></a>Ebenenobjekt (ADO MD)
Enthält eine Menge von Elementen, von die jedes denselben Rang innerhalb einer Hierarchie besitzt.  
  
## <a name="remarks"></a>Hinweise  
 Die Auflistungen und Eigenschaften einer **Ebene** -Objekts können Sie folgende Möglichkeiten:  
  
-   Identifizieren der **Ebene** mit der [Namen](../../../ado/reference/ado-md-api/name-property-ado-md.md) und [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) Eigenschaften.  
  
-   Zurückgeben einer Zeichenfolge beim Anzeigen verwendet die **Ebene** mit der [Beschriftung](../../../ado/reference/ado-md-api/caption-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben einer sinnvollen Zeichenfolge, die beschreibt die **Ebene** mit der [Beschreibung](../../../ado/reference/ado-md-api/description-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben der [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekte, aus denen die **Ebene** mit der [Elemente](../../../ado/reference/ado-md-api/members-collection-ado-md.md) Auflistung.  
  
-   Die Anzahl der Ebenen zurück, aus dem Stammverzeichnis der **Ebene** mit der [Tiefe](../../../ado/reference/ado-md-api/depth-property-ado-md.md) Eigenschaft.  
  
-   Verwenden Sie das standardmäßige ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) -Auflistung, um zusätzliche Informationen zu erhalten die **Ebene** Objekt.  
  
 Die **Eigenschaften** Auflistung enthält Eigenschaften, die vom Anbieter bereitgestellt. Die folgende Tabelle enthält Eigenschaften, die möglicherweise zur Verfügung. Die tatsächliche Eigenschaftenliste kann je nach der Implementierung des Anbieters abweichen. Siehe die Dokumentation für Ihren Anbieter für eine vollständige Liste der verfügbaren Eigenschaften.  
  
|Name|Description|  
|----------|-----------------|  
|CatalogName|Der Name des Katalogs, zu dem dieser Cube gehört.|  
|CubeName|Der Name des Cubes.|  
|Description|Eine aussagekräftige Beschreibung der Ebene.|  
|DimensionUniqueName|Der eindeutige Name des der [Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Der eindeutige Name der Hierarchie.|  
|LevelCaption|Eine Bezeichnung oder Beschriftung, die der Ebene zugeordnet.|  
|LevelCardinality|Die Anzahl der Elemente in der Ebene.|  
|LevelGUID|Die GUID der Ebene.|  
|LevelName|Der Name der Ebene.|  
|LevelNumber|Der Abstand zwischen der Ebene und den Stamm der Hierarchie.|  
|LevelType|Der Typ der Ebene.|  
|LevelUniqueName|Der eindeutige Name der Ebene.|  
|SchemaName|Der Name des Schemas, zu dem dieser Cube gehört.|  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CubeDef-Beispiel (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Hierarchy-Objekt (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Levels-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Members-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
