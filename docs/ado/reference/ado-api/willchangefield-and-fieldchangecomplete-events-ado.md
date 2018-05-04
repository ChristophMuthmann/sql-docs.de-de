---
title: WillChangeField- und FieldChangeComplete-Ereignisse (ADO) | Microsoft Docs
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
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0114851f666589df614cbec9ba279ccfa0313189
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField- und FieldChangeComplete-Ereignisse (ADO)
Die **WillChangeField** Ereignis wird aufgerufen, bevor ein ausstehender Vorgang verwendet den Wert einer oder mehrerer ändert [Feld](../../../ado/reference/ado-api/field-object.md) Objekte in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Die **FieldChangeComplete** Ereignis wird aufgerufen, nachdem der Wert aus einem oder mehreren **Feld** Objekte wurde geändert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *cFields*  
 Ein **lange** , der angibt, dass der Anzahl der **Feld** Objekte im *Felder*.  
  
 *Fields*  
 Für **WillChangeField**, *Felder* Parameter ist ein Array von **Varianten** enthält **Feld** Objekte mit den ursprünglichen Werten. Für **FieldChangeComplete**, *Felder* Parameter ist ein Array von **Varianten** enthält **Feld** Objekte mit den geänderten Werten .  
  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn aufgetretenen Fehlers beschrieben der Wert der *AdStatus* ist **AdStatusErrorsOccurred**; andernfalls ist es nicht festgelegt.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert.  
  
 Wenn **WillChangeField** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat, erfolgreich war. Es wird festgelegt, um **AdStatusCantDeny** Wenn dieses Ereignis den Abbruch des ausstehenden Vorgangs anfordern kann.  
  
 Wenn **FieldChangeComplete** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, oder auf **AdStatusErrorsOccurred** Wenn der Vorgang ist fehlgeschlagen.  
  
 Vor dem **WillChangeField** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusCancel** auf den Abbruch der Anforderung des ausstehenden Vorgangs.  
  
 Vor dem **FieldChangeComplete** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pRecordset*  
 Ein **Recordset** Objekt. Die **Recordset** für die dieses Ereignis aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Ein **WillChangeField** oder **FieldChangeComplete** Ereignis kann auftreten, der zum Einstellen der [Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft und der Aufruf der [Update](../../../ado/reference/ado-api/update-method.md) Methode mit Arrayparametern Feld und Wert.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)
