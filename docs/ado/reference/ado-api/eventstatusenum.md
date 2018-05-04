---
title: EventStatusEnum | Microsoft Docs
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
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1fa1f613008c12d684c0af7f65e13988c8baf16
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="eventstatusenum"></a>EventStatusEnum
Gibt den aktuellen Status der Ausführung eines Ereignisses an.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|Fordert den Abbruch des Vorgangs, der das Ereignis ausgelöst hat.|  
|**adStatusCantDeny**|3|Gibt an, dass der Vorgang nicht Abbrechen des ausstehenden Vorgangs anfordern kann.|  
|**adStatusErrorsOccurred**|2|Gibt an, dass der Vorgang, der das Ereignis ausgelöst wurde aufgrund eines Fehlers oder Fehlern fehlgeschlagen ist.|  
|**adStatusOK**|1|Gibt an, dass der Vorgang, der das Ereignis verursacht hat erfolgreich war.|  
|**adStatusUnwantedEvent**|5|Verhindert, dass nachfolgende Benachrichtigungen vor der Ausführung die Ereignismethode beendet wurde.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.EventStatus.CANCEL|  
|AdoEnums.EventStatus.CANTDENY|  
|AdoEnums.EventStatus.ERRORSOCCURRED|  
|AdoEnums.EventStatus.OK|  
|AdoEnums.EventStatus.UNWANTEDEVENT|  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[BeginTransComplete-, CommitTransComplete- und RollbackTransComplete-Ereignisse (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete- und Disconnect-Ereignis (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[EndOfRecordset-Ereignis (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[ExecuteComplete-Ereignis (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[FetchComplete-Ereignis (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[InfoMessage-Ereignis (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[WillChangeField- und FieldChangeComplete-Ereignis (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[WillChangeRecord- und RecordChangeComplete-Ereignis (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset- und RecordsetChangeComplete-Ereignis (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillConnect-Ereignis (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[WillExecute-Ereignis (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[WillMove- und MoveComplete-Ereignis (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
