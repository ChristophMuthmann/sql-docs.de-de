---
title: EOS-Eigenschaft | Microsoft Docs
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
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c29c72e9cd88ff5672b90aeab5da97c7742f5b30
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="eos-property"></a>EOS-Eigenschaft
Gibt an, ob die aktuelle Position am Ende der [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **booleschen** -Wert, der angibt, ob die aktuelle Position am Ende des Streams ist. **EOS** gibt **"true"** es sind keine weitere Bytes im Datenstrom; gibt **"false"** treten mehr Bytes, die nach der aktuellen Position.  
  
 Um das Ende des Streamposition festzulegen, verwenden die [SetEOS](../../../ado/reference/ado-api/seteos-method.md) Methode. Verwenden Sie zum Bestimmen der aktuellen Position der [Position](../../../ado/reference/ado-api/position-property-ado.md) Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [EOS und Zeilentrennzeichen Eigenschaften und SkipLine-Methode (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
