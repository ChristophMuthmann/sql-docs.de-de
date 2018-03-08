---
title: CubeDef-Objekt (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea97010f67e571ddf9ddfb1dcc1cf36e38769710
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="cubedef-object-ado-md"></a>CubeDef-Objekt (ADO MD)
Stellt einen Cube aus einem mehrdimensionalen Schema mit einem Satz von verknüpften Dimensionen dar.  
  
## <a name="remarks"></a>Hinweise  
 Die Auflistungen und Eigenschaften einer **CubeDef** -Objekts können Sie folgende Möglichkeiten:  
  
-   Identifizieren einer **CubeDef** mit der [Namen](../../../ado/reference/ado-md-api/name-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben einer Zeichenfolge, die den Cube beschreibt die [Beschreibung](../../../ado/reference/ado-md-api/description-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben der Dimensionen, die den Cube mit bilden die [Dimensionen](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) Auflistung.  
  
-   Zusätzliche Informationen zum Abrufen der **CubeDef** mit dem standard ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
 Die **Eigenschaften** Auflistung enthält Eigenschaften, die vom Anbieter bereitgestellt. Die folgende Tabelle enthält Eigenschaften, die möglicherweise zur Verfügung. Die tatsächliche Eigenschaftenliste kann je nach der Implementierung des Anbieters abweichen. Siehe die Dokumentation für Ihren Anbieter für eine vollständige Liste der verfügbaren Eigenschaften.  
  
|Name|Description|  
|----------|-----------------|  
|CatalogName|Der Name des Katalogs, zu dem dieser Cube gehört.|  
|CreatedOn|Datum und Uhrzeit der Erstellung des Cubes.|  
|CubeGUID|Die GUID des Cubes.|  
|CubeName|Der Name des Cubes.|  
|CubeType|Der Typ des Cubes.|  
|DataUpdatedBy|Der Benutzername der Person, die auf diese Weise der letzten datenaktualisierung.|  
|Description|Eine aussagekräftige Beschreibung des Cubes.|  
|LastSchemaUpdate|Datum und Uhrzeit der letzten Aktualisierung des Schemas.|  
|SchemaName|Der Name des Schemas, zu dem dieser Cube gehört.|  
|SchemaUpdatedBy|Benutzer-ID der Person, die auf diese Weise die Aktualisierung des letzten Schemas.|  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CubeDef-Beispiel (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Katalogobjekt (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Auflistung von Dimensionen (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
