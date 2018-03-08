---
title: WillMove- und MoveComplete-Ereignisse (ADO) | Microsoft Docs
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
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac06472367c1ebb000d317a6373ea911241e45f8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove- und MoveComplete-Ereignisse (ADO)
Die **WillMove** Ereignis wird aufgerufen, bevor ein ausstehender Vorgang ändert sich die aktuelle Position in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Die **MoveComplete** Ereignis wird aufgerufen, nachdem die aktuelle Position in der **Recordset** ändert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameter  
 *adReason*  
 Ein [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) Wert, der die Ursache für dieses Ereignis angibt. Der Wert kann **AdRsnMoveFirst**, **AdRsnMoveLast**, **AdRsnMoveNext**, **AdRsnMovePrevious**, **AdRsnMove** , oder **AdRsnRequery**.  
  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn aufgetretenen Fehlers beschrieben der Wert der *AdStatus* ist **AdStatusErrorsOccurred**; andernfalls wird der Parameter nicht festgelegt.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert.  
  
 Wenn **WillMove** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat, erfolgreich war. Es wird festgelegt, um **AdStatusCantDeny** Wenn dieses Ereignis den Abbruch des ausstehenden Vorgangs anfordern kann.  
  
 Wenn **MoveComplete** wird aufgerufen, wird dieser Parameter auf festgelegt **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, oder auf **AdStatusErrorsOccurred** Wenn die Fehler bei Vorgang.  
  
 Vor dem **WillMove** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusCancel** Abbruch des ausstehenden Vorgangs anzufordern oder legen Sie diesen Parameter auf **AdStatusUnwantedEvent** nachfolgende Benachrichtigungen zu verhindern.  
  
 Vor dem **MoveComplete** zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pRecordset*  
 Ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Die **Recordset** für die dieses Ereignis aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 Ein **WillMove** oder **MoveComplete** Ereignis kann auftreten, aufgrund der folgenden **Recordset** Operations: [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Verschieben](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), und [Requery](../../../ado/reference/ado-api/requery-method.md). Diese Ereignisse können auftreten, aufgrund der folgenden Eigenschaften: [Filter](../../../ado/reference/ado-api/filter-property.md), [Index](../../../ado/reference/ado-api/index-property.md), [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), und [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md). Diese Ereignisse auch auftreten, wenn ein untergeordnetes Element **Recordset** hat **Recordset** Ereignisse verbunden und das übergeordnete Element **Recordset** verschoben wird.  
  
 Müssen Sie festlegen der *AdStatus* Parameter **AdStatusUnwantedEvent** für jeden möglichen *AdReason* Wert, um die ereignisbenachrichtigung für jedes Ereignis vollständig zu beenden, enthält eine *AdReason* Parameter.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
