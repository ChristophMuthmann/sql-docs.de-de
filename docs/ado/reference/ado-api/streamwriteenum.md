---
title: StreamWriteEnum | Microsoft Docs
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
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b81765d125680bc52a8e95adcb3828df36bfc0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Gibt an, ob eine Linie wird als Trennzeichen an die Zeichenfolge angefügt wird eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Standard. Schreibt die angegebene Textzeichenfolge (gemäß der *Daten* Parameter), die **Stream** Objekt.|  
|**adWriteLine**|1|Schreibt eine Zeichenfolge und ein Zeilentrennzeichen zu einem **Stream** Objekt. Wenn die [Zeilentrennzeichen](../../../ado/reference/ado-api/lineseparator-property-ado.md) Eigenschaft ist nicht definiert, und klicken Sie dann einen Laufzeitfehler zurückgegeben.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [WriteText-Methode](../../../ado/reference/ado-api/writetext-method.md)
