---
title: StreamWriteEnum | Microsoft Docs
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
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36c18f5452a07e5dc44a9396ee993a163b98d3bd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
