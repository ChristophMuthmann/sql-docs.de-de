---
title: Read-Methode | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords: Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 740be677f54f8d4b5d30902a792b58d4681df888
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
