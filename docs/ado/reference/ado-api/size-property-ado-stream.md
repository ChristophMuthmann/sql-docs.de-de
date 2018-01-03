---
title: Size-Eigenschaft (ADO-Datenstrom) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::Size
helpviewer_keywords: Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0a58ee1c4e425af65518a1be5d8629acc849c67
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Size-Eigenschaft (ADO Parameter)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
