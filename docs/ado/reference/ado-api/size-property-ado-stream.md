---
title: Size-Eigenschaft (ADO-Datenstrom) | Microsoft Docs
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
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c5a4027bf589a469092a6605743df3d08147e7d2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="size-property-ado-stream"></a>Eigenschaft "Größe" (ADO-Datenstrom)
Gibt die Größe des Streams in Anzahl von Bytes an.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **lange** Wert, der die Größe des Datenstroms in Anzahl von Bytes angibt. Der Standardwert ist die Größe des Streams oder -1, wenn die Größe des Datenstroms nicht bekannt ist.  
  
## <a name="remarks"></a>Hinweise  
 **Größe** können verwendet werden, nur mit geöffneter [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekte.  
  
> [!NOTE]
>  Eine beliebige Anzahl von Bits gespeichert werden kann, einer **Stream** -Objekt, durch die verfügbaren Systemressourcen begrenzt. Wenn die **Stream** enthält mehr Bits, als durch dargestellt werden kann ein **lange** Wert **Größe** abgeschnitten, und daher wird nicht einwandfrei an die Länge der **Stream**.  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenschaft "Größe" (ADO-Parameter)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
