---
title: Hierarchy-Objekt (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Hierarchy
helpviewer_keywords: Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e02aefb90af923cea7bfd6d33b8b1e97415c6ae8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy-Objekt (ADO MD)
Stellt eine Möglichkeit dar, in dem die Mitglieder einer [Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) aggregiert werden können oder die "Rollup wird erstellt." Eine Dimension kann entlang einer oder mehrerer Hierarchien aggregiert werden.  
  
## <a name="remarks"></a>Hinweise  
 Die Auflistungen und Eigenschaften einer **Hierarchie** -Objekts können Sie folgende Möglichkeiten:  
  
-   Identifizieren der **Hierarchie** mit der [Namen](../../../ado/reference/ado-md-api/name-property-ado-md.md) und [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) Eigenschaften.  
  
-   Zurückgeben einer sinnvollen Zeichenfolge, die beschreibt die **Hierarchie** mit der [Beschreibung](../../../ado/reference/ado-md-api/description-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben der [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) Objekte, aus denen die **Hierarchie** mit der [Ebenen](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) Auflistung.  
  
-   Verwenden Sie das standardmäßige ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) -Auflistung, um zusätzliche Informationen zu erhalten die **Hierarchie** Objekt.  
  
 Die **Eigenschaften** Auflistung enthält Eigenschaften, die vom Anbieter bereitgestellt. Die folgende Tabelle enthält Eigenschaften, die möglicherweise zur Verfügung. Die tatsächliche Eigenschaftenliste kann je nach der Implementierung des Anbieters abweichen. Siehe die Dokumentation für Ihren Anbieter für eine vollständige Liste der verfügbaren Eigenschaften.  
  
|Name|Description|  
|----------|-----------------|  
|AllMember|Das Element auf höchster Ebene des Rollups in der Hierarchie.|  
|CatalogName|Der Name des Katalogs, zu dem dieser Cube gehört.|  
|CubeName|Der Name des Cubes.|  
|DefaultMember|Der eindeutige Name des Standardelements für diese Hierarchie.|  
|Description|Eine aussagekräftige Beschreibung der Hierarchie.|  
|DimensionType|Der Typ der Dimension, zu dem diese Hierarchie gehört.|  
|DimensionUniqueName|Der eindeutige Name der Dimension.|  
|HierarchyCaption|Eine Bezeichnung oder Beschriftung, die der Hierarchie zugeordnet ist.|  
|HierarchyCardinality|Die Anzahl der Member in der Hierarchie.|  
|HierarchyGUID|Die GUID der Hierarchie.|  
|HierarchyName|Der Name der Hierarchie.|  
|HierarchyUniqueName|Der eindeutige Name der Hierarchie.|  
|SchemaName|Der Name des Schemas, zu dem dieser Cube gehört.|  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CubeDef-Beispiel (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Dimensionsobjekt (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Hierarchies-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Levels-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
