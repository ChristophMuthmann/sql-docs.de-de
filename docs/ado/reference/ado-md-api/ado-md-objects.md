---
title: ADO MD-Objekte | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4a0fa75a3b03b2cb5f2a31ed3bdf3756e1c64b01
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-md-objects"></a>ADO MD-Objekte
|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Stellt eine mit Feldern fester Breite oder Filterachse eines cellSets, ausgewählte Elemente der eine oder mehrere Dimensionen enthält.|  
|[Katalog](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Mehrdimensionale Schemainformationen (Cubes und zugrunde liegende Dimensionen, Hierarchien, Ebenen und Elemente), die speziell für eine mehrdimensionale Datenanbieter (MDP) enthält.|  
|[Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Stellt die Daten am Schnittpunkt der Achsenkoordinaten, enthalten im Cellset dar.|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Stellt die Ergebnisse einer MDX-Abfrage. Es ist eine Ansammlung von Zellen, die aus Cubes oder anderen Cellsets ausgewählt wurden.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Stellt einen Cube aus einem mehrdimensionalen Schema mit einem Satz von verknüpften Dimensionen dar.|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Stellt eine der Dimensionen eines mehrdimensionalen Cubes, die, die eine oder mehrere Hierarchien von Elementen enthält.|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Stellt eine Möglichkeit dar, in dem die Elemente einer Dimension können aggregiert oder "Rollup wird erstellt." Eine Dimension kann entlang einer oder mehrerer Hierarchien aggregiert werden.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Enthält eine Menge von Elementen, von die jedes denselben Rang innerhalb einer Hierarchie besitzt.|  
|[Datenmember](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Stellt ein Element einer Ebene in einem Cube die untergeordneten Elemente eines Elements einer Ebene oder ein Mitglied einer Position auf einer Achse eines cellSets dar.|  
|[Position](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Stellt einen Satz von ein oder mehrere Elemente verschiedener Dimensionen, der einen Punkt auf einer Achse definiert.|  
  
 Darüber hinaus die **Katalog** -Objekt verbunden ist, um eine ADO **Verbindung** -Objekt, das mit der ADO-Standardbibliothek enthalten ist:  
  
|Objekt|Description|  
|------------|-----------------|  
|[Verbindung](../../../ado/reference/ado-api/connection-object-ado.md)|Stellt eine offene Verbindung mit einer Datenquelle dar.|  
  
 Die Beziehungen zwischen diesen Objekten werden veranschaulicht, der [ADO MD-Objektmodell](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Viele ADO MD-Objekte können in eine entsprechende Auflistung enthalten sein. Z. B. eine [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) Objekt enthalten sein kann, einem [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) Auflistung von einer **Katalog**. Weitere Informationen finden Sie unter [ADO MD-Auflistungen](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ADO MD-API-Referenz](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD-Codebeispiele](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD-Auflistungen](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD-Enumerationskonstanten](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD-Methoden](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD-Objektmodell](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD-Eigenschaften](../../../ado/reference/ado-md-api/ado-md-properties.md)
