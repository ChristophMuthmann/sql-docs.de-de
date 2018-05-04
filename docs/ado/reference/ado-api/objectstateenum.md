---
title: ObjectStateEnum | Microsoft Docs
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
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a8d7ba4da1908d2434049c8a71039a259bab8ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
