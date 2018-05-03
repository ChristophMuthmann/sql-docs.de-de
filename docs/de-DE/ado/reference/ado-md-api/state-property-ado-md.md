---
title: State-Eigenschaft (ADO MD) | Microsoft Docs
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
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1960818e3ebf5b58610e18bfb23ee7c8c3101b8e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
