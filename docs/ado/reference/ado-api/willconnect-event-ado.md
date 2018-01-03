---
title: WillConnect-Ereignis (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords: WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45e9a6fb4dcc55b836195065c279627e50c74511
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="willconnect-event-ado"></a>WillConnect-Ereignis (ADO)
Die **WillConnect** Ereignis wird aufgerufen, bevor eine Verbindung gestartet wird.  
  
 **Gilt für:** [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameter  
 *"ConnectionString"*  
 Ein **Zeichenfolge** , die Verbindungsinformationen für die ausstehende Verbindung enthält.  
  
 *Benutzer-ID*  
 Ein **Zeichenfolge** , einen Benutzernamen für die ausstehende Verbindung enthält.  
  
 *Kennwort*  
 Ein **Zeichenfolge** , ein Kennwort für die ausstehende Verbindung enthält.  
  
 *enthalten*  
 Ein **lange** Wert, der angibt, wie der Anbieter auswerten soll die *"ConnectionString"*. Ihre einzige Option ist **AdAsyncOpen**.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert.  
  
 Wenn dieses Ereignis aufgerufen wird, wird dieser Parameter festgelegt, um **AdStatusOK** standardmäßig. Es wird festgelegt, um **AdStatusCantDeny** , wenn das Ereignis den Abbruch des ausstehenden Vorgangs anfordern kann.  
  
 Bevor Sie dieses Ereignis zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern. Legen Sie diesen Parameter auf **AdStatusCancel** zur Anforderung des Verbindung-Vorgangs, der Abbruch von dieser Benachrichtigung verursacht hat.  
  
 *pConnection*  
 Die [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt für den dieser ereignisbenachrichtigung gilt. Änderungen an den Parametern des der **Verbindung** durch die **WillConnect** -Ereignishandler hat keine Auswirkung auf die **Verbindung**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn **WillConnect** aufgerufen wird, die *"ConnectionString"*, *UserID*, *Kennwort*, und *Optionen* Parameter werden festgelegt, auf die Werte, die durch die der Vorgang, der dieses Ereignis (die ausstehende Verbindung) und kann geändert werden, bevor das Ereignis zurückgegeben. **WillConnect** gelegten eine Anforderung, dass die ausstehende Verbindung abgebrochen werden.  
  
 Wenn dieses Ereignis abgebrochen wird, **ConnectComplete** wird aufgerufen, mit dessen *AdStatus* Parametersatz auf **AdStatusErrorsOccurred**.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)
