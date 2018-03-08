---
title: FetchComplete-Ereignis (ADO) | Microsoft Docs
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
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8332a6332f27a8e2022975a80814be9c28cf4da
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete-Ereignis (ADO)
Die **FetchComplete** Ereignis wird aufgerufen, nachdem alle Datensätze in einer langen asynchronen Operation in abgerufen wurden die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn aufgetretenen Fehlers beschrieben der Wert der **AdStatus** ist **AdStatusErrorsOccurred**; andernfalls ist es nicht festgelegt.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert. Wenn dieses Ereignis aufgerufen wird, wird dieser Parameter festgelegt, um **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, oder auf **AdStatusErrorsOccurred** bei fehlgeschlagenem Vorgang.  
  
 Bevor Sie dieses Ereignis zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pRecordset*  
 Ein **Recordset** Objekt. Das Objekt, für das die Datensätze abgerufen wurden.  
  
## <a name="remarks"></a>Hinweise  
 Mit **FetchComplete** mit Microsoft Visual Basic, Visual Basic 6.0 oder höher ist erforderlich.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)
