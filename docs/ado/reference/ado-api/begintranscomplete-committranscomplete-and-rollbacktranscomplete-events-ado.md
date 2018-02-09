---
title: BeginTrans, CommitTrans, RollbackTrans Ereignisse (ADO) | Microsoft Docs
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
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2bc471f7a401d42e2ae11462d526d0686da0d49
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete-, CommitTransComplete- und RollbackTransComplete-Ereignisse (ADO)
Diese Ereignisse werden aufgerufen, nachdem der zugeordnete Vorgang auf der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt die Ausführung abgeschlossen ist.  
  
-   **BeginTransComplete** wird aufgerufen, nachdem die [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Vorgang.  
  
-   **CommitTransComplete** wird aufgerufen, nachdem die [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Vorgang.  
  
-   **RollbackTransComplete** wird aufgerufen, nachdem die [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Vorgang.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameter  
 *TransactionLevel*  
 Ein **lange** -Wert, der die neue Transaktionsebene enthält die **BeginTrans** , die dieses Ereignis verursacht hat.  
  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Es beschreibt den Fehler, die aufgetreten sind, wenn der Wert von EventStatusEnum **AdStatusErrorsOccurred**; andernfalls ist es nicht festgelegt.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert. Wenn eines dieser Ereignisse aufgerufen wird, wird dieser Parameter festgelegt, um **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, oder auf **AdStatusErrorsOccurred** bei fehlgeschlagenem Vorgang.  
  
 Diese Ereignisse können zu verhindern, dass nachfolgende Benachrichtigungen durch Festlegen dieses Parameters auf **AdStatusUnwantedEvent** vor dem Ereignis wird zurückgegeben.  
  
 *pConnection*  
 Die **Verbindung** -Objekt für die dieses Ereignis aufgetreten ist.  
  
## <a name="remarks"></a>Hinweise  
 In Visual C++ mehrere **Verbindungen** können die gleiche Ereignisbehandlungsmethode freigeben. Die Methode verwendet den zurückgegebenen **Verbindung** Objekts bestimmen, welches Objekt das Ereignis verursacht hat.  
  
 Wenn die [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) -Eigenschaftensatz auf **AdXactCommitRetaining** oder **AdXactAbortRetaining**, eine neue Transaktion nach dem Commit oder Rollback einer Transaktion startet. Verwenden der **BeginTransComplete** Ereignis, um alle ignorieren jedoch die erste Transaktion Start-Ereignis.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans, CommitTrans und RollbackTrans-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans-, CommitTrans- und RollbackTrans-Methode (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
