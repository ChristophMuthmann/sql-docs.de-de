---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ObjectStateEnum
helpviewer_keywords: ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa1236357042126f60b27f4c6f943ae3c2198bb0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="objectstateenum"></a>ObjectStateEnum
Gibt an, ob ein Objekt offen oder geschlossen, Herstellen einer Verbindung mit einer Datenquelle, die Ausführung eines Befehls oder Abrufen von Daten.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Gibt an, dass das Objekt geschlossen wird.|  
|**adStateOpen**|1|Gibt an, dass das Objekt geöffnet ist.|  
|**adStateConnecting**|2|Gibt an, dass das Objekt eine Verbindung herstellt.|  
|**adStateExecuting**|4|Gibt an, dass das Objekt einen Befehl ausgeführt wird.|  
|**adStateFetching**|8|Gibt an, dass die Zeilen des Objekts abgerufen werden.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[State-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State-Eigenschaft (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
