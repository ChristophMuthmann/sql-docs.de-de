---
title: Children-Eigenschaft (ADO MD) | Microsoft Docs
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
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39c1ba30aab6f6a972241c0e564a7a0680165828
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="children-property-ado-md"></a>Children-Eigenschaft (ADO MD)
Gibt eine [Elemente](../../../ado/reference/ado-md-api/members-collection-ado-md.md) Auflistung, für die aktuelle [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) ist das übergeordnete Element in der Hierarchie.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **Elemente** Auflistung und ist schreibgeschützt.  
  
## <a name="remarks"></a>Hinweise  
 Der **untergeordneten Elemente** Eigenschaft enthält eine **Mitglieder** Auflistung, für die aktuelle **Member** hierarchische übergeordnet ist. Blattelemente Ebene **Member** Objekte verfügen über keine untergeordneten Elemente der **Elemente** Auflistung. Diese Eigenschaft wird nur unterstützt, auf **Member** Objekte für eine [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) Objekt. Ein Fehler tritt auf, wenn diese Eigenschaft, von verwiesen wird **Member** Objekte für eine [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) Objekt.  
  
## <a name="applies-to"></a>Gilt für  
 [Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ChildCount-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
