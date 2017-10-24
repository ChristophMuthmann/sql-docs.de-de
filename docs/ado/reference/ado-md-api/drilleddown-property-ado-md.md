---
title: DrilledDown-Eigenschaft (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8dfa880e78bdeccf722723a7d05f2f0ca1938ed6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

