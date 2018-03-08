---
title: Ordinal-Eigenschaft (ADO MD Zelle) | Microsoft Docs
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
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70c8bb0793791873663c561ccafcdc37bcb37b8a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
