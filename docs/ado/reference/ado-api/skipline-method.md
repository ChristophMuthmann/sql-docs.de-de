---
title: SkipLine-Methode | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
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
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a24691a7579efd5585ccecf413158273354152cd
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="skipline-method"></a>SkipLine-Methode
Überspringt eine gesamte Zeile beim Lesen von Text [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Hinweise  
 Alle Zeichen bis zur und einschließlich der nächsten Linie wird als Trennzeichen werden übersprungen. Wird standardmäßig die [Zeilentrennzeichen](../../../ado/reference/ado-api/lineseparator-property-ado.md) ist **AdCRLF**. Wenn Sie versuchen, überspringen [EOS](../../../ado/reference/ado-api/eos-property.md), bleibt die aktuelle Position am **EOS**.  
  
 Die **SkipLine** Methode wird verwendet, mit dem Text-Streams ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**).  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
