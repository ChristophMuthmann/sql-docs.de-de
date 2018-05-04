---
title: Zeilentrennzeichen-Eigenschaft (ADO) | Microsoft Docs
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
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3c82ab9eccb144f3b8615b8c813eb84f9150024
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="lineseparator-property-ado"></a>Zeilentrennzeichen-Eigenschaft (ADO)
Gibt die binären Zeichen als Zeilentrennzeichen in Text zu verwendende [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekte.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) -Wert, der das Zeilentrennzeichen verwendet wird, der **Stream**. Der Standardwert ist **AdCRLF**.  
  
## <a name="remarks"></a>Hinweise  
 **Zeilentrennzeichen** wird verwendet, um Zeilen zu interpretieren, wenn den Inhalt von Text zu lesen **Stream**. Zeilen können übersprungen werden, mit der [SkipLine](../../../ado/reference/ado-api/skipline-method.md) Methode.  
  
 **Zeilentrennzeichen** wird verwendet, nur mit Text **Stream** Objekte ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**). Diese Eigenschaft wird ignoriert, wenn **Typ** ist **AdTypeBinary**.  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
