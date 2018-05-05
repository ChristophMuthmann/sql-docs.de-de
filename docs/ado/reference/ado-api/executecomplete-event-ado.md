---
title: ExecuteComplete-Ereignis (ADO) | Microsoft Docs
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
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab8c0b33fe31499999cc73d2ebc03ef0d32ace70
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete-Ereignis (ADO)
Die **ExecuteComplete** Ereignis wird aufgerufen, nachdem ein Befehl beendet wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parameter  
 *RecordsAffected*  
 Ein **lange** Wert, der angibt, der Anzahl der Datensätze, die von dem Befehl betroffen sind.  
  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn aufgetretenen Fehlers beschrieben der Wert der **AdStatus** ist **AdStatusErrorsOccurred**; andernfalls ist es nicht festgelegt.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert. Wenn dieses Ereignis aufgerufen wird, wird dieser Parameter festgelegt, um **AdStatusOK** , wenn der Vorgang, der das Ereignis verursacht hat erfolgreich war, oder auf **AdStatusErrorsOccurred** bei fehlgeschlagenem Vorgang.  
  
 Bevor Sie dieses Ereignis zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** um nachfolgende Benachrichtigungen zu verhindern.  
  
 *pCommand*  
 Die [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objekt, das ausgeführt wurde. Enthält eine **Befehl** Objekt auch beim Aufrufen von **Connection.Execute** oder **Recordset.Open** ohne explizites erstellen eine **Befehl** , in welchen Fällen die **Befehl** -Objekt intern durch ADO erstellt wurde.  
  
 *pRecordset*  
 Ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, das das Ergebnis des Befehls ausgeführt wird. Dies **Recordset** kann leer sein. Sie sollten dieses Recordset-Objekt innerhalb dieser Ereignishandler nie gelöscht. Andernfalls wird eine zugriffsverletzung entstehen, wenn ADO versucht, Zugriff auf ein Objekt, das nicht mehr vorhanden ist.  
  
 *pConnection*  
 Ein [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt. Die Verbindung, über die Sie der Vorgang ausgeführt wurde.  
  
## <a name="remarks"></a>Hinweise  
 Ein **ExecuteComplete** Ereignis kann auftreten, aufgrund der **Verbindung.** [Ausführen](../../../ado/reference/ado-api/execute-method-ado-connection.md), **Befehl.** [Ausführen](../../../ado/reference/ado-api/execute-method-ado-command.md), **Recordset.** [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md), **Recordset.** [Requery](../../../ado/reference/ado-api/requery-method.md), oder **Recordset.** [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md) Methoden.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)
