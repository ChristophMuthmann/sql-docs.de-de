---
title: Read-Methode | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: reference
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
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e73ea6c8a837322b10aeea877eef10ba37a0b560
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="read-method"></a>Read-Methode
Liest eine angegebene Anzahl von Bytes aus einer Binärdatei [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parameter  
 *NumBytes*  
 Optional. Ein **lange** Wert, der angibt, die Anzahl der Bytes, die aus der Datei gelesen oder [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) Wert **AdReadAll**, dies ist die Standardeinstellung.  
  
## <a name="return-value"></a>Rückgabewert  
 Die **lesen** Methode liest eine angegebene Anzahl von Bytes oder die gesamte Datenstrom aus einer **Stream** Objekt und gibt die resultierenden Daten als ein **Variant**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn *NumBytes* verbleiben länger als die Anzahl der Bytes in der **Stream**, werden nur die verbleibende Bytes zurückgegeben. Die gelesenen Daten werden nicht entsprechend die vom angegebenen Länge aufgefüllt *NumBytes*. Wenn keine um zu lesenden Bytes sind, wird eine Variante mit einem null-Wert zurückgegeben. **Lesen** kann nicht verwendet werden, um rückwärts zu lesen.  
  
> [!NOTE]
>  *NumBytes* immer misst Bytes. Für Text **Stream** Objekte ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**), verwenden Sie [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ReadText-Methode](../../../ado/reference/ado-api/readtext-method.md)
