---
title: StreamOpenOptionsEnum | Microsoft Docs
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
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0e30eeeba1cfcbafe66fc26d24456697c693638
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Gibt Optionen zum Öffnen einer [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt. Die Werte können mit einer OR-Operation kombiniert werden.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Öffnet die **Stream** Objekt im asynchronen Modus ausgeführt.|  
|**adOpenStreamFromRecord**|4|Identifiziert den Inhalt der *Quelle* Parameter bereits geöffnet sein [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt. Das Standardverhalten besteht, behandeln *Quelle* als eine URL, die direkt mit einem Knoten in einer Struktur verweist. Der diesem Knoten zugeordnete Standarddatenstrom wird geöffnet.|  
|**adOpenStreamUnspecified**|-1|Standard. Gibt an, öffnen die **Stream** Objekt mit den Standardoptionen.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [Open-Methode (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)
