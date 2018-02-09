---
title: Description-Eigenschaft (ADO MD) | Microsoft Docs
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
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f3052ab5b0ad05c1a792ff348e77ea0b32c7484
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="description-property-ado-md"></a>Description-Eigenschaft (ADO MD)
Gibt eine Erläuterung der Text des aktuellen Objekts zurück.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **Zeichenfolge** und ist schreibgeschützt.  
  
## <a name="remarks"></a>Hinweise  
 Für [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekte **Beschreibung** gilt nur für Measures und Formeln Member. **Beschreibung** gibt eine leere Zeichenfolge ("") für alle anderen Typen von Elementen. Weitere Informationen zu den verschiedenen Typen von Elementen finden Sie unter der [Typ](../../../ado/reference/ado-md-api/type-property-ado-md.md) Eigenschaft.  
  
 Diese Eigenschaft wird nur unterstützt, auf **Member** Objekte, die zu gehören eine [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) Objekt. Ein Fehler tritt auf, wenn diese Eigenschaft, von verwiesen wird **Member** Objekte für eine [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) Objekt.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[CubeDef-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Dimensionsobjekt (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Hierarchy-Objekt (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Level-Objekt (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
