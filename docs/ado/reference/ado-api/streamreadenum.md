---
title: StreamReadEnum | Microsoft Docs
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
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32b606d6f960dc77f8d90257b8c18d19703620d9
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="streamreadenum"></a>StreamReadEnum
Gibt an, ob der gesamte Datenstrom oder die nächste Zeile aus gelesen werden soll eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Standard. Liest alle Bytes aus dem Stream, aus der aktuellen Position bis zur der [EOS](../../../ado/reference/ado-api/eos-property.md) Marker. Dies ist der einzige gültige **StreamReadEnum** Wert mit binäre Datenströme ([Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) ist **AdTypeBinary**).|  
|**adReadLine**|-2|Liest die nächste Zeile aus dem Datenstrom (gekennzeichnet durch die [Zeilentrennzeichen](../../../ado/reference/ado-api/lineseparator-property-ado.md) Eigenschaft).|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Read-Methode](../../../ado/reference/ado-api/read-method.md)|[ReadText-Methode](../../../ado/reference/ado-api/readtext-method.md)|
