---
title: WillChangeRecordset- und RecordsetChangeComplete-Ereignisse (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a3ff0f75d5e9ef9d71e4eb2a103367a97f263d8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset- und RecordsetChangeComplete-Ereignisse (ADO)
Die **WillChangeRecordset** Ereignis wird aufgerufen, bevor ein ausstehender Vorgang ändert die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Die **RecordsetChangeComplete** Ereignis wird aufgerufen, nachdem die **Recordset** hat sich geändert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *adReason*  
 Ein [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) Wert, der die Ursache für dieses Ereignis angibt. Der Wert kann **AdRsnRequery**, **AdRsnResynch**, **AdRsnClose**, **AdRsnOpen**.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert.  
  
 Wenn **WillChangeRecordset** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat, erfolgreich war. Es wird festgelegt, um **AdStatusCantDeny** Wenn dieses Ereignis den Abbruch des ausstehenden Vorgangs anfordern kann.  
  
 Wenn **RecordsetChangeComplete** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, **AdStatusErrorsOccurred** Wenn der Vorgang fehlgeschlagen ist, oder **AdStatusCancel** Wenn der Vorgang mit der zuvor zugelassene zugeordnete **WillChangeRecordset** Ereignis abgebrochen wurde.  
  
 Vor dem **WillChangeRecordset** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusCancel** zum Abbruch des ausstehenden Vorgangs anzufordern, oder legen Sie diesen Parameter, zu verhindern, dass nachfolgende Benachrichtigungen werden gesendet.  
  
 Vor dem **WillChangeRecordset** oder **RecordsetChangeComplete** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn aufgetretenen Fehlers beschrieben der Wert der *AdStatus* ist **AdStatusErrorsOccurred**; andernfalls ist es nicht festgelegt.  
  
 *pCommand*  
 Ein **Recordset** Objekt. Die **Recordset** für die dieses Ereignis aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Ein **WillChangeRecordset** oder **RecordsetChangeComplete** Ereignis kann auftreten, weil die **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md) oder [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methoden.  
  
 Wenn der Anbieter keine Lesezeichen unterstützt eine **RecordsetChange** ereignisbenachrichtigung tritt immer dann, die neue Zeilen vom Anbieter abgerufen werden. Die Häufigkeit dieses Ereignisses hängt die **RecordsetCacheSize** Eigenschaft.  
  
 Sie müssen festlegen, der **AdStatus** Parameter an **AdStatusUnwantedEvent** für jeden möglichen **AdReason** Wert vollständig ereignisbenachrichtigung für jedes Ereignis beendet wurde, die enthält ein **AdReason** Parameter.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)

