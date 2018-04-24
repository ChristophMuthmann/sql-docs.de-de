---
title: Dimension-Objekt (ADO MD) | Microsoft Docs
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
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4818afd2bbf7392385c3516be1d762266cd2b60
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="dimension-object-ado-md"></a>Dimensionsobjekt (ADO MD)
Stellt eine der Dimensionen eines mehrdimensionalen Cubes, die, die eine oder mehrere Hierarchien von Elementen enthält.  
  
## <a name="remarks"></a>Hinweise  
 Die Auflistungen und Eigenschaften einer **Dimension** -Objekts können Sie folgende Möglichkeiten:  
  
-   Identifizieren der **Dimension** mit der [Namen](../../../ado/reference/ado-md-api/name-property-ado-md.md) und [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) Eigenschaften.  
  
-   Zurückgeben einer sinnvollen Zeichenfolge, die beschreibt die **Dimension** mit der [Beschreibung](../../../ado/reference/ado-md-api/description-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben der [Hierarchie](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) Objekte, aus denen die **Dimension** mit der [Hierarchien](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) Auflistung.  
  
-   Verwenden Sie das standardmäßige ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) -Auflistung, um zusätzliche Informationen zu erhalten die **Dimension** Objekt.  
  
 Die **Eigenschaften** Auflistung enthält Eigenschaften, die vom Anbieter bereitgestellt. Die folgende Tabelle enthält Eigenschaften, die möglicherweise zur Verfügung. Die tatsächliche Eigenschaftenliste kann je nach der Implementierung des Anbieters abweichen. Siehe die Dokumentation für Ihren Anbieter für eine vollständige Liste der verfügbaren Eigenschaften.  
  
|Name|Description|  
|----------|-----------------|  
|CatalogName|Der Name des Katalogs, zu dem dieser Cube gehört.|  
|CubeName|Der Name des Cubes.|  
|Standardhierarchie|Der eindeutige Name der Standardhierarchie.|  
|Description|Eine aussagekräftige Beschreibung des Cubes.|  
|DimensionCaption|Eine Bezeichnung oder Beschriftung, die der Dimension zugeordnet werden soll.|  
|DimensionCardinality|Die Anzahl der Elemente in der Dimension.|  
|DimensionGUID|Die GUID der Dimension.|  
|DimensionName|Der Name der Dimension.|  
|DimensionOrdinal|Die Ordinalzahl der Dimension innerhalb dieser Gruppe von Dimensionen, die den Cube zu bilden.|  
|DimensionType|Die Dimension-Datentyp.|  
|DimensionUniqueName|Der eindeutige Name der Dimension.|  
|SchemaName|Der Name des Schemas, zu dem dieser Cube gehört.|  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CubeDef-Beispiel (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Auflistung von Dimensionen (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Hierarchies-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
