---
title: SetEOS-Methode | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 600625802c16c8e6860c462fe369f70eb9c1805c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="seteos-method"></a>SetEOS-Methode
Legt die Position, die das Ende des Streams fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Hinweise  
 **SetEOS** aktualisiert den Wert der [EOS](../../../ado/reference/ado-api/eos-property.md) Eigenschaft, indem Sie die aktuelle [Position](../../../ado/reference/ado-api/position-property-ado.md) das Ende des Streams. Alle Bytes oder Zeichen nach der aktuellen Position werden abgeschnitten.  
  
 Da [schreiben](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md), und [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) in vorhandenen zusätzlichen Werte werden nicht abgeschnitten **Stream** Objekte aufweist, können Sie diese kürzen Byte- oder Zeichensequenz durch Festlegen der neuen Position der End-of-Stream mit **SetEOS**.  
  
> [!CAUTION]
>  Wenn Sie festlegen, **EOS** auf eine Position vor dem tatsächlichen Ende des Streams, alle Daten verloren nach neuen **EOS** Position.  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
