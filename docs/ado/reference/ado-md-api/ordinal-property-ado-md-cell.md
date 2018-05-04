---
title: Ordinal-Eigenschaft (ADO MD Zelle) | Microsoft Docs
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
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f0e483f0d2154902c56e36cbbaf1962f2dc3d6a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal-Eigenschaft (ADO MD Zelle)
Identifiziert eindeutig eine [Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md) anhand seiner Position innerhalb eines cellSets dar.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **lange** Integer und ist schreibgeschützt.  
  
## <a name="remarks"></a>Hinweise  
 Ordnungswert der Zelle identifiziert Zelle eindeutig, die innerhalb eines cellSets dar. Grundsätzlich werden Zellen in einem Cellset nummeriert, als wäre das Cellset ein *p*-dimensionales Array, in dem *p* ist die Anzahl der [Achsen](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). Zellen werden beginnend mit 0 (null) in zeilengerichteter Reihenfolge nummeriert. Hier wird die Formel zum Berechnen der Ordinalzahl einer Zelle ein:  
  
 Ordnungswert der Zelle verwendet werden kann, mit der [Element](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) Eigenschaft von der [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) Objekt schnell abgerufen werden die [Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Cell-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Achse-Beispiel (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Eigenschaft "Element" (ADO MD Cellset)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal-Eigenschaft (ADO MD Position)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
