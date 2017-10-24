---
title: Zeilentrennzeichen-Eigenschaft (ADO) | Microsoft Docs
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
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2be2e27fa93791647fd3e27945c3203cf1afe999
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="lineseparator-property-ado"></a>Zeilentrennzeichen-Eigenschaft (ADO)
Gibt die binären Zeichen als Zeilentrennzeichen in Text zu verwendende [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekte.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) -Wert, der das Zeilentrennzeichen verwendet wird, der **Stream**. Der Standardwert ist **AdCRLF**.  
  
## <a name="remarks"></a>Hinweise  
 **Zeilentrennzeichen** wird verwendet, um Zeilen zu interpretieren, wenn den Inhalt von Text zu lesen **Stream**. Zeilen können übersprungen werden, mit der [SkipLine](../../../ado/reference/ado-api/skipline-method.md) Methode.  
  
 **Zeilentrennzeichen** wird verwendet, nur mit Text **Stream** Objekte ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeText**). Diese Eigenschaft wird ignoriert, wenn **Typ** ist **AdTypeBinary**.  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)

