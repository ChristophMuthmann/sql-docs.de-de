---
title: Write-Methode | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77b4da5ba900cdd3456bbfe611ea0fe1021e23d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="write-method"></a>Write-Methode
Schreibt binäre Daten in einem [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parameter  
 *Buffer*  
 Ein **Variant** , die ein Array von zu schreibenden Bytes enthält.  
  
## <a name="remarks"></a>Hinweise  
 Angegebenen Bytes geschrieben werden, um die **Stream** Objekts ohne Leerzeichen zwischen den einzelnen Byte.  
  
 Die aktuelle [Position](../../../ado/reference/ado-api/position-property-ado.md) festgelegt ist, auf das Byte, die geschriebenen Daten folgt. Die **schreiben** -Methode werden die restlichen Daten in einem Datenstrom nicht abgeschnitten. Wenn Sie diese Bytes abschneiden möchten, rufen [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Wenn Sie nach der aktuellen schreiben [EOS](../../../ado/reference/ado-api/eos-property.md) Position der [Größe](../../../ado/reference/ado-api/size-property-ado-stream.md) von der **Stream** wird erhöht werden, um alle neuen Bytes enthalten und **EOS** wird verschoben um die neue letzte Byte in den **Stream**.  
  
> [!NOTE]
>  Die **schreiben** Methode mit binäre Datenströme verwendet wird ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeBinary**). Für Textstreams (**Typ** ist **AdTypeText**), verwenden Sie [WriteText](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [WriteText-Methode](../../../ado/reference/ado-api/writetext-method.md)
