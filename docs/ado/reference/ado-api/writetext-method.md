---
title: WriteText-Methode | Microsoft Docs
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
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords: WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c744551b835ce814f8a6baf9781e04e67b6139d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="writetext-method"></a>WriteText-Methode
Schreibt eine angegebene Zeichenfolge an eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parameter  
 *Daten*  
 Ein **Zeichenfolge** Wert, der den Text in der zu schreibenden Zeichen enthält.  
  
 *enthalten*  
 Optional. Ein [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) Wert, der angibt, ob ein Zeilentrennzeichen am Ende der angegebenen Zeichenfolge geschrieben werden muss.  
  
## <a name="remarks"></a>Hinweise  
 Angegebene Zeichenfolgen werden geschrieben, um die **Stream** Objekt ohne dazwischenliegende Leerzeichen oder Zeichen zwischen den einzelnen Zeichenfolgen.  
  
 Die aktuelle [Position](../../../ado/reference/ado-api/position-property-ado.md) festgelegt ist, auf das Zeichen, die geschriebenen Daten folgt. Die **WriteText** -Methode werden die restlichen Daten in einem Datenstrom nicht abgeschnitten. Wenn diese Zeichen abgeschnitten werden sollen, rufen Sie [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Wenn Sie nach der aktuellen schreiben [EOS](../../../ado/reference/ado-api/eos-property.md) Position der [Größe](../../../ado/reference/ado-api/size-property-ado-stream.md) von der **Stream** wird erhöht werden, um alle neuen Zeichen enthalten und **EOS** Wechselt in die neue letzte Byte in den **Stream**.  
  
> [!NOTE]
>  Die **WriteText** Methode wird verwendet, mit dem Text-Streams ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**). Für binäre Datenströme (**Typ** ist **AdTypeBinary**), verwenden Sie [schreiben](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Write-Methode](../../../ado/reference/ado-api/write-method.md)
