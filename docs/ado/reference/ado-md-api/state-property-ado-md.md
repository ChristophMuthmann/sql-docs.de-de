---
title: State-Eigenschaft (ADO MD) | Microsoft Docs
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
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1886dae43bdb764a67fa5e44b1e8fe9744c0cb5f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="state-property-ado-md"></a>State-Eigenschaft (ADO MD)
Gibt den aktuellen Status der das Cellset an.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **lange** ganze Zahl, die den aktuellen Zustand, der angibt, die [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) -Objekt und ist schreibgeschützt. Die folgenden Werte sind gültig: **AdStateClosed** (0) und **AdStateOpen** (1).  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) Konstantennamen, benötigen Sie die ADO-Typbibliothek in Ihrem Projekt referenziert. Finden Sie unter [mithilfe von ADO mit ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) für Weitere Informationen.  
  
## <a name="applies-to"></a>Gilt für  
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Close-Methode (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open-Methode (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
