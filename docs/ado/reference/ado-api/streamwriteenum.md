---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 586920fc4f7673f9c5e25c92f252013920acaa8d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

