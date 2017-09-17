---
title: Type-Eigenschaft (ADO-Datenstrom) | Microsoft Docs
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
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b16d683d9e5460e5aba904a8bc4ccc7362b2287
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="type-property-ado-stream"></a>Type-Eigenschaft (ADO-Datenstrom)
Gibt den Typ der Daten in der [Stream](../../../ado/reference/ado-api/stream-object-ado.md) (binär oder Text).  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) Wert, der angibt, den Typ der Daten in der **Stream** Objekt. Der Standardwert ist **AdTypeText**. Wenn die Binärdaten in ein neues anfänglich geschrieben werden, jedoch leer ist **Stream**, die **Typ** wird geändert in **AdTypeBinary**.  
  
## <a name="remarks"></a>Hinweise  
 Die **Typ** Eigenschaft ist Lese-/Schreibzugriff nur, wenn die aktuelle Position am Anfang ist der **Stream** ([Position](../../../ado/reference/ado-api/position-property-ado.md) ist 0), "und" Read-only an einer beliebigen anderen Position.  
  
 Die**Typ** Eigenschaft bestimmt, welche Methoden verwendet werden soll, zum Lesen und Schreiben der **Stream**. Für Text **Streams**, verwenden Sie [ReadText](../../../ado/reference/ado-api/readtext-method.md) und [WriteText](../../../ado/reference/ado-api/writetext-method.md). Für binäre **Streams**, verwenden Sie [lesen](../../../ado/reference/ado-api/read-method.md) und [schreiben](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [RecordType-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type-Eigenschaft (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
