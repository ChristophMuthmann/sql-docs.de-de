---
title: DrilledDown-Eigenschaft (ADO MD) | Microsoft Docs
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
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8be1a63b9d4f1c979d7670c2ed3a79766070ca4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown-Eigenschaft (ADO MD)
Gibt an, ob die untergeordneten Elemente unmittelbar folgen der [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) auf der Achse.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **booleschen** -Wert und ist schreibgeschützt. **DrilledDown** gibt **"true"** , wenn keine untergeordneten Elemente des aktuellen Elements auf der Achse vorhanden sind. **DrilledDown** gibt **"false"** verfügt das aktuelle Element einen oder mehrere untergeordnete Elemente auf der Achse.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **DrilledDown** Eigenschaft, um zu bestimmen, ob mindestens ein untergeordnetes Element dieses Elements auf der Achse unmittelbar nach diesem Element vorhanden ist. Diese Informationen sind nützlich, wenn das Element angezeigt.  
  
 Diese Eigenschaft wird nur unterstützt, auf [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekte für eine [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) Objekt. Ein Fehler tritt auf, wenn diese Eigenschaft, von verwiesen wird **Member** Objekte für eine [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) Objekt.  
  
## <a name="applies-to"></a>Gilt für  
 [Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ParentSameAsPrev-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
