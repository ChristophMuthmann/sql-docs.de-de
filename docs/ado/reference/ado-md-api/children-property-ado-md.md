---
title: Children-Eigenschaft (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c851f06ecd3cec67769f761cb2aea400c5b06d9e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

