---
title: Member-Objekt (ADO MD) | Microsoft Docs
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
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e198438a1e1b3c0375daf0cb955d68aeddadae0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="member-object-ado-md"></a>Member-Objekt (ADO MD)
Stellt ein Element einer Ebene in einem Cube die untergeordneten Elemente eines Elements einer Ebene oder ein Mitglied einer Position auf einer Achse eines cellSets dar.  
  
## <a name="remarks"></a>Hinweise  
 Die Eigenschaften einer **Member** unterscheiden sich je nach Zusammenhang, in dem er verwendet wird. Ein **Member** von einer [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) in eine [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) hat eine [untergeordneten Elemente](../../../ado/reference/ado-md-api/children-property-ado-md.md) Eigenschaft, die zurückgibt der **Mitglieder** auf die nächsten untergeordneten Ebene der Hierarchie aus der aktuellen **Member**. Für eine **Member** von einer [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md), die **Kinder** Sammlung ist stets leer. Darüber hinaus die [Typ](../../../ado/reference/ado-md-api/type-property-ado-md.md) Eigenschaft gilt nur für **Elemente** von einer **Ebene**.  
  
 Ein **Member** von **Position** verfügt über zwei Eigenschaften, die nützlich beim Anzeigen sind der [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) und [ ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Wird eine Fehlermeldung angezeigt, wenn der Zugriff auf diese Eigenschaften auf eine **Member** von einer **Ebene**.  
  
 Die Auflistungen und Eigenschaften von einer **Member** Objekt vom eine **Ebene**, können Sie wie folgt vorgehen:  
  
-   Identifizieren der **Member** mit der [Namen](../../../ado/reference/ado-md-api/name-property-ado-md.md) und [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) Eigenschaften.  
  
-   Zurückgeben einer Zeichenfolge beim Anzeigen verwendet die **Member** mit der [Beschriftung](../../../ado/reference/ado-md-api/caption-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben einer sinnvollen Zeichenfolge, die ein Measure oder eine Formel beschreibt **Member** mit der [Beschreibung](../../../ado/reference/ado-md-api/description-property-ado-md.md) Eigenschaft.  
  
-   Ermitteln Sie die Art von der **Member** mit der [Typ](../../../ado/reference/ado-md-api/type-property-ado-md.md) Eigenschaft.  
  
-   Abrufen von Informationen zu den **Ebene** von der **Member** mit der [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) und [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) Eigenschaften.  
  
-   Abrufen verwandte **Elemente** in einer [Hierarchie](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) mit der [übergeordneten](../../../ado/reference/ado-md-api/parent-property-ado-md.md) und [untergeordneten Elemente](../../../ado/reference/ado-md-api/children-property-ado-md.md) Eigenschaften.  
  
-   Anzahl der untergeordneten Elemente ein **Member** mit der [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) Eigenschaft.  
  
-   Verwenden Sie das standardmäßige ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) -Auflistung, um zusätzliche Informationen zu erhalten die **Ebene** Objekt.  
  
 Die Auflistungen und Eigenschaften der eine **Member** von eine **Position** entlang einer [Achse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), können Sie wie folgt vorgehen:  
  
-   Identifizieren der **Member** mit der [Namen](../../../ado/reference/ado-md-api/name-property-ado-md.md) und [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) Eigenschaften.  
  
-   Zurückgeben einer Zeichenfolge beim Anzeigen verwendet die **Member** mit der [Beschriftung](../../../ado/reference/ado-md-api/caption-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben einer sinnvollen Zeichenfolge, die ein Measure oder eine Formel beschreibt **Member** mit der [Beschreibung](../../../ado/reference/ado-md-api/description-property-ado-md.md) Eigenschaft.  
  
-   Abrufen von Informationen zu den **Ebene** von der **Member** mit der [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) und [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) Eigenschaften.  
  
-   Anzahl der untergeordneten Elemente ein **Member** mit der [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) Eigenschaft.  
  
-   Verwenden der [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) Eigenschaft, um zu bestimmen, ob es ist mindestens ein untergeordnetes Element auf der **Achse** unmittelbar folgt **Member**.  
  
-   Verwenden der [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) -Eigenschaft können Sie bestimmen, ob das übergeordnete Element dieses **Member** ist identisch mit das übergeordnete Element des unmittelbar vorangehenden **Member**.  
  
-   Verwenden Sie das standardmäßige ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) -Auflistung, um zusätzliche Informationen zu erhalten die **Ebene** Objekt.  
  
 Die **Eigenschaften** Auflistung enthält Eigenschaften, die vom Anbieter bereitgestellt. Die folgende Tabelle enthält Eigenschaften, die möglicherweise zur Verfügung. Die tatsächliche Eigenschaftenliste kann je nach der Implementierung des Anbieters abweichen. Siehe die Dokumentation für Ihren Anbieter für eine vollständige Liste der verfügbaren Eigenschaften.  
  
|Name|Description|  
|----------|-----------------|  
|CatalogName|Der Name des Katalogs, zu dem dieser Cube gehört.|  
|ChildrenCardinality|Die Anzahl der untergeordneten Elemente des Elements.|  
|CubeName|Der Name des Cubes.|  
|Description|Eine aussagekräftige Beschreibung des Elements.|  
|DimensionUniqueName|Der eindeutige Name des der [Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Der eindeutige Name der Hierarchie.|  
|LevelNumber|Der Abstand zwischen der Ebene und den Stamm der Hierarchie.|  
|LevelUniqueName|Der eindeutige Name der Ebene.|  
|MemberCaption|Eine Bezeichnung oder Beschriftung, die dem Element zugeordnet ist.|  
|MemberGUID|Die GUID des Elements.|  
|MemberName|Der Name des Elements.|  
|MemberOrdinal|Die Ordinalzahl des Elements.|  
|MemberType|Der Typ des Elements.|  
|MemberUniqueName|Der eindeutige Name des Elements.|  
|ParentCount|Die Anzahl der übergeordneten Elemente dieses Elements.|  
|ParentLevel|Die Nummer der Ebene des übergeordneten Element.|  
|ParentUniqueName|Der eindeutige Name des dem Element übergeordneten Elements.|  
|SchemaName|Der Name des Schemas, zu dem dieser Cube gehört.|  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Katalog-Beispiel (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Members-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
