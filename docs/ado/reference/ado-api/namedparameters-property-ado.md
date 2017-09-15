---
title: NamedParameters-Eigenschaft (ADO) | Microsoft Docs
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
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 613f4cb52c6225d573d314b83f26c220e7caabfc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="namedparameters-property-ado"></a>NamedParameters-Eigenschaft (ADO)
Gibt an, ob Parameternamen an den Anbieter übergeben werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn diese Eigenschaft auf "true" festgelegt ist, wird ADO übergibt den Wert des der **Name** -Eigenschaft jedes Parameters im der **Parameter** Auflistung für die [Befehlsobjekt](../../../ado/reference/ado-api/command-object-ado.md). Der Anbieter verwendet einen Parameternamen ein Parameter entsprechend der **CommandText** oder **CommandStream** Eigenschaften. Wenn diese Eigenschaft auf "false" festgelegt ist (Standardeinstellung), Parameternamen werden ignoriert, und der Anbieter verwendet die Reihenfolge der Parameter entsprechend der Werte für Parameter in der **CommandText** oder **CommandStream** Eigenschaften.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters-Auflistung (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
