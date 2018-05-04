---
title: NamedParameters-Eigenschaft (ADO) | Microsoft Docs
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
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c64c7ee4bf239ca3084417724209ad715d63eeda
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="namedparameters-property-ado"></a>NamedParameters-Eigenschaft (ADO)
Gibt an, ob Parameternamen an den Anbieter übergeben werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn diese Eigenschaft auf "true" festgelegt ist, wird ADO übergibt den Wert des der **Name** -Eigenschaft jedes Parameters im der **Parameter** Auflistung für die [Befehlsobjekt](../../../ado/reference/ado-api/command-object-ado.md). Der Anbieter verwendet einen Parameternamen ein Parameter entsprechend der **CommandText** oder **CommandStream** Eigenschaften. Wenn diese Eigenschaft auf "false" festgelegt ist (Standardeinstellung), Parameternamen werden ignoriert, und der Anbieter verwendet die Reihenfolge der Parameter entsprechend der Werte für Parameter in der **CommandText** oder **CommandStream** Eigenschaften.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters-Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
