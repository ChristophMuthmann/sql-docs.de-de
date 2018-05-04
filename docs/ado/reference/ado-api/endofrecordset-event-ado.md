---
title: EndOfRecordset-Ereignis (ADO) | Microsoft Docs
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
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f035d61d2e8526c21960761be2db5a900666083c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset-Ereignis (ADO)
Die **EndOfRecordset** Ereignis wird immer dann aufgerufen, wenn der Versuch zum Verschieben einer Zeile nach dem Ende der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *fMoreData*  
 Ein **VARIANT_BOOL** -Wert, wenn auf VARIANT_TRUE festgelegt ist, gibt an, mehr Zeilen wurden hinzugefügt, um die **Recordset**.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert.  
  
 Wenn **EndOfRecordset** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat, erfolgreich war. Es wird festgelegt, um **AdStatusCantDeny** Falls dieses Ereignis kann nicht der Abbruch des Vorgangs angefordert werden, die dieses Ereignis verursacht hat.  
  
 Vor dem **EndOfRecordset** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pRecordset*  
 Ein **Recordset** Objekt. Die **Recordset** für die dieses Ereignis aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Ein **EndOfRecordset** Ereignis kann auftreten, wenn die [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) -Vorgang fehl.  
  
 Dieser Ereignishandler wird aufgerufen, wenn versucht wird, verschieben Sie das Ende der **Recordset** -Objekt, z. B. als Ergebnis **MoveNext**. Allerdings klicken Sie in diesem Fall wird Sie könnten mehr Datensätze aus einer Datenbank abrufen und hängt sie an das Ende der **Recordset**. In diesem Fall legen *fMoreData* auf VARIANT_TRUE fest, und der Rückgabewert von **EndOfRecordset**. Rufen Sie anschließend **MoveNext** erneut aus, um die neu abgerufener Datensätze zugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)
