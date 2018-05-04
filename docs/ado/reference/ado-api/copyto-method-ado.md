---
title: CopyTo-Methode (ADO) | Microsoft Docs
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
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32e889ea84c02a544ccad53cd9c274c360994bfe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="copyto-method-ado"></a>CopyTo-Methode (ADO)
Kopiert die angegebene Anzahl von Zeichen oder Bytes (je nach [Typ](../../../ado/reference/ado-api/type-property-ado-stream.md)) in der [Stream](../../../ado/reference/ado-api/stream-object-ado.md) in eine andere **Stream** Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parameter  
 *DestStream*  
 Der Wert einer Objektvariable, die einen Verweis auf ein offenes enthält **Stream** Objekt. Die aktuelle **Stream** wird an das Ziel kopiert **Stream** gemäß *DestStream*. Das Ziel **Stream** bereits geöffnet sein. Falls nicht, tritt ein Laufzeitfehler auf.  
  
> [!NOTE]
>  Die *DestStream* Parameter möglicherweise einen Proxy nicht **Stream** Objekt, da dies den Zugriff auf eine private Schnittstelle auf erfordert die **Stream** -Objekt, das nicht möglich Remoteausführung auf die Client.  
  
 *NumChars*  
 Optional. Ein **Ganzzahl** Wert, der angibt, die Anzahl von Bytes oder Zeichen aus der aktuellen Position in der Quelle zu kopierenden **Stream** an das Ziel **Stream**. Der Standardwert ist -1, der angibt, dass alle Zeichen oder Bytes, aus der aktuellen Position bis kopiert werden [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode kopiert die angegebene Anzahl von Zeichen oder Bytes, beginnend mit der aktuellen Position gemäß der [Position](../../../ado/reference/ado-api/position-property-ado.md) Eigenschaft. Wenn die angegebene Anzahl größer als die Anzahl der Bytes bis verfügbaren ist **EOS**, und klicken Sie dann nur die Zeichen oder Bytes aus der aktuellen Position bis **EOS** beim Übertragungsvorgang kopiert werden. Wenn der Wert der *NumChars* – 1 ist oder weggelassen wird, werden alle Zeichen oder Bytes ab, die von der aktuellen Position kopiert.  
  
 Wenn vorhandene Zeichen oder Bytes in den Zieldatenstrom, werden alle Inhalte über den Zeitpunkt, an dem der Kopiervorgang endet, hinaus bleiben, und werden nicht abgeschnitten. **Position** das Byte, das unmittelbar hinter das letzte Byte kopiert wird. Wenn Sie diese Bytes abschneiden möchten, rufen [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** sollte verwendet werden, um Daten in ein Ziel kopiert **Stream** desselben Typs als Quelle **Stream** (ihre **Typ** eigenschafteneinstellungen werden beide **AdTypeText** oder beides **AdTypeBinary**). Für Text **Stream** Objekte aufweist, können Sie ändern die [Charset](../../../ado/reference/ado-api/charset-property-ado.md) eigenschafteneinstellung des Ziels **Stream** Übersetzen von einem Zeichen in eine andere festgelegt. Außerdem Text **Stream** Objekte können in binären erfolgreich kopiert werden **Stream** Objekte aber binäre **Stream** Objekte können nicht kopiert werden, in Text **Stream**  Objekte.  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
