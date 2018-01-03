---
title: WillChangeRecord- und RecordChangeComplete-Ereignisse (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 522d2385cc2670ed940768f7584d3c9eb7942748
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord- und RecordChangeComplete-Ereignisse (ADO)
Die **WillChangeRecord** Ereignis aufgerufen wird, bevor eine oder mehrere Datensätze (Zeilen) in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ändern. Die **RecordChangeComplete** Ereignis wird aufgerufen, nachdem eine oder mehrere Einträge ändern.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *adReason*  
 Ein [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) Wert, der die Ursache für dieses Ereignis angibt. Der Wert kann **AdRsnAddNew**, **AdRsnDelete**, **AdRsnUpdate**, **AdRsnUndoUpdate**, **AdRsnUndoAddNew**, **AdRsnUndoDelete**, oder **AdRsnFirstChange**.  
  
 *cRecords*  
 Ein **lange** Wert, der die Anzahl der Datensätze ändern (betroffen) angibt.  
  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn aufgetretenen Fehlers beschrieben der Wert der *AdStatus* ist **AdStatusErrorsOccurred**; andernfalls ist es nicht festgelegt.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert.  
  
 Wenn **WillChangeRecord** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat, erfolgreich war. Es wird festgelegt, um **AdStatusCantDeny** Wenn dieses Ereignis den Abbruch des ausstehenden Vorgangs anfordern kann.  
  
 Wenn **RecordChangeComplete** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, oder auf **AdStatusErrorsOccurred** Wenn der Vorgang ist fehlgeschlagen.  
  
 Vor dem **WillChangeRecord** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusCancel** Anforderung Abbruch des Vorgangs, der dieses Ereignis verursacht hat, oder legen Sie diesen Parameter zu  **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 Vor dem **RecordChangeComplete** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pCommand*  
 Ein **Recordset** Objekt. Die **Recordset** für die dieses Ereignis aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Ein **WillChangeRecord** oder **RecordChangeComplete** Ereignis kann auftreten, für das erste geänderte Feld in einer Zeile aufgrund der folgenden **Recordset** Operations: [ Update](../../../ado/reference/ado-api/update-method.md), [löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), und [ CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). Der Wert, der die **Recordset** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) bestimmt, welche Vorgänge dazu führen, dass die Ereignisse auftreten.  
  
 Während der **WillChangeRecord** Ereignis, das **Recordset** [Filter](../../../ado/reference/ado-api/filter-property.md) -Eigenschaftensatz auf **AdFilterAffectedRecords**. Diese Eigenschaft kann nicht geändert werden, während das Ereignis verarbeitet.  
  
 Sie müssen festlegen, der **AdStatus** Parameter an **AdStatusUnwantedEvent** für jeden möglichen **AdReason** Wert vollständig ereignisbenachrichtigung für jedes Ereignis beendet wurde, die enthält ein **AdReason** Parameter.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)
