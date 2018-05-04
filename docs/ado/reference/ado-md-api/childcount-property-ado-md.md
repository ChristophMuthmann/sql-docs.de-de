---
title: ChildCount-Eigenschaft (ADO MD) | Microsoft Docs
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
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93052e44fdf7ce5e939478f9822653696dcc1b76
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="childcount-property-ado-md"></a>ChildCount-Eigenschaft (ADO MD)
Gibt die Anzahl der Elemente für den aktuellen [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekt ist das übergeordnete Element in einer Hierarchie.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **lange** Integer und ist schreibgeschützt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **ChildCount** -Eigenschaft zum Zurückgeben von Schätzung für wie viele untergeordnete Elemente einer **Member** hat. Die tatsächliche untergeordneten Elemente ein **Member** zurückgegeben werden kann, indem die [untergeordneten Elemente](../../../ado/reference/ado-md-api/children-property-ado-md.md) Eigenschaft.  
  
 Für **Member** Objekte aus einer [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) Objekt ist, wird die maximale Anzahl zurückgegeben wird, 65536. Wenn die tatsächliche Anzahl der Kinder 65536 überschreitet, wird der zurückgegebene Wert immer noch 65536 sein. Aus diesem Grund sollte die Anwendung interpretieren einer **ChildCount** von 65.536 als oder gleich 65536 untergeordnete Elemente.  
  
 Für **Member** Objekte aus einer [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) Objekt, das die Auflistung von ADO verwenden, [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft auf die **untergeordneten Elemente** Auflistung, um zu bestimmen, die genaue Anzahl der untergeordneten Elemente. Bestimmen die genaue Anzahl der untergeordneten Elemente ist möglicherweise langsam, wenn die Anzahl der untergeordneten Elemente in der Auflistung groß ist.  
  
## <a name="applies-to"></a>Gilt für  
 [Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Children-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count-Eigenschaft (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Members-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
