---
title: Ereignisparameter | Microsoft Docs
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
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5351c36af4082c40be10b451122ca04101cf4b3d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="event-parameters"></a>Ereignisparameter
Jeder Ereignishandler hat einen Status-Parameter, der steuert, den Ereignishandler an. Für Ereignisse durch Abschluss wird dieser Parameter auch verwendet, um anzugeben, den Erfolg oder Misserfolg des Vorgangs, der das Ereignis generiert hat. Möglichst lückenlos Ereignisse enthalten auch einen Fehlerparameter enthalten Informationen zu Fehlern, die möglicherweise aufgetreten und einen oder mehrere Objektparameter, die an den ADO-Objekten, die zum Ausführen des Vorgangs zu verweisen. Z. B. die [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) Ereignis enthält die Objektparameter für die **Befehl**, **Recordset**, und **Verbindung** Objekte mit dem Ereignis verknüpft sind. Im folgenden Beispiel von Microsoft® Visual Basic® finden Sie unter der pCommand pCommand und pConnection-Objekten, die darstellen der **Befehl**, **Recordset**, und **Verbindung** Objekte, mit denen, die **Execute** Methode.  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 Mit Ausnahme der **Fehler** -Objekt, auf die Ereignisse werden die gleichen Parameter übergeben werden. Mit diesem können Sie jedes der Objekte untersuchen, die in den ausstehenden Vorgang verwendet werden und zu bestimmen, ob der Vorgang abgeschlossen werden darf.  
  
 Einige Ereignishandler weisen eine *Grund* -Parameter, der enthält zusätzliche Informationen darüber, warum das Ereignis aufgetreten ist. Z. B. die **WillMove** und **MoveComplete** Ereignisse können auftreten, weil eine der Navigationsmethoden (**MoveNext**, **MovePrevious**usw.) aufgerufen wird oder als Ergebnis eine erneute Abfrage.  
  
## <a name="status-parameter"></a>Status-Parameter  
 Wenn die Ereignishandler-Routine aufgerufen wird, die *Status* Parameter auf einen der folgenden Werte festgelegt ist.  
  
|Wert|Description|  
|-----------|-----------------|  
|**adStatusOK**|Übergeben wird und Ereignisse durch Abschluss. Dieser Wert bedeutet, dass den Vorgang, der das Ereignis wurde erfolgreich abgeschlossen verursacht.|  
|**adStatusErrorsOccurred**|Um nur Ereignisse durch Abschluss übergeben. Dieser Wert bedeutet, dass der Vorgang, der das Ereignis verursacht hat, nicht erfolgreich war, oder ein Ereignisses wird der Vorgang wurde abgebrochen. Überprüfen Sie die *Fehler* -Parameter für weitere Details.|  
|**adStatusCantDeny**|Wird nur auf Ereignisse übergeben. Dieser Wert bedeutet, dass das Ereignis wird der Vorgang abgebrochen werden kann nicht an. Sie müssen ausgeführt werden.|  
  
 Wenn Sie in das Ereignis wird, die der Vorgang fortgesetzt werden soll bestimmen, lassen Sie die *Status* -Parameter unverändert. Solange der eingehende Statusparameter nicht, um festgelegt wurde **AdStatusCantDeny**, Sie können jedoch den ausstehenden Vorgang abbrechen, indem ändern *Status* auf **AdStatusCancel**. Wenn Sie dies tun, das dem Vorgang zugeordnete Abschlussereignis hat seine *Status* Parametersatz auf **AdStatusErrorsOccurred**. Die **Fehler** Objekt, das das ausgelöste Ereignis übergeben den Wert enthält **AdErrOperationCancelled**.  
  
 Wenn Sie ein Ereignis verarbeitet nicht mehr verwenden möchten, legen Sie *Status* auf **AdStatusUnwantedEvent** und Ihre Anwendung nicht mehr benachrichtigt, wenn das Ereignis empfangen. Beachten Sie jedoch, dass einige Ereignisse, die mehr als ein Grund ausgelöst werden können. In diesem Fall müssen Sie angeben **AdStatusUnwantedEvent** für jede mögliche Ursache. Beispielsweise zum Beenden des Empfangs der Benachrichtigung über ausstehende **RecordChange** Ereignisse, die Sie festlegen müssen die *Status* Parameter **AdStatusUnwantedEvent** für  **AdRsnAddNew**, **AdRsnDelete**, **AdRsnUpdate**, **AdRsnUndoUpdate**, **AdRsnUndoAddNew**, **AdRsnUndoDelete**, und **AdRsnFirstChange** , wenn sie auftreten.  
  
|Wert|Description|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|Fordern Sie an, dass dieser Ereignishandler keine weiteren Benachrichtigungen erhalten.|  
|**adStatusCancel**|Anfordern der Abbruch des Vorgangs, die durchgeführt wird.|  
  
## <a name="error-parameter"></a>Fehlerparameter  
 Die *Fehler* Parameter ist ein Verweis auf ein ADO [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Wenn die *Status* Parameter auf festgelegt ist **AdStatusErrorsOccurred**, die **Fehler** Objekt enthält die Details, warum der Vorgang fehlgeschlagen ist. Das wird Ereignis zugeordneten ausgelöste Ereignis. den Vorgang durch Festlegen von abgebrochen hat die *Status* Parameter an **AdStatusCancel**, das Fehlerobjekt ist immer auf festgelegt  **AdErrOperationCancelled**.  
  
## <a name="object-parameter"></a>Object-Parameter  
 Jedes Ereignis empfängt ein oder mehrere Objekte, die im Vorgang betroffenen Objekten darstellt. Z. B. die **ExecuteComplete** -Ereignis empfängt ein **Befehl** -Objekt, eine **Recordset** -Objekt, und ein **Verbindung** Objekt.  
  
## <a name="reason-parameter"></a>Reason-Parameter  
 Die *Grund* Parameter *AdReason*, enthält zusätzliche Informationen darüber, warum das Ereignis aufgetreten ist. Ereignisse mit einem *AdReason* Parameter kann auch für den gleichen Vorgang aus, für einen anderen Grund jedes Mal mehrere Male aufgerufen werden. Z. B. die **WillChangeRecord** Ereignishandler wird aufgerufen, für die Vorgänge, die sind im Begriff, führen Sie "oder" Rückgängig einfügen, löschen oder Ändern eines Datensatzes. Wenn Sie ein Ereignis zu verarbeiten, nur wenn es keinen bestimmten Grund auftritt, können Sie verwenden möchten die *AdReason* Parameter herausfiltern, die Vorkommen Sie nicht interessiert sind. Z. B. Wenn Sie zum Verarbeiten von Datensatz-Change-Ereignissen nur, wenn sie auftreten, da ein Eintrag hinzugefügt wurde, können Sie etwa wie folgt verwenden.  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 In diesem Fall kann die Benachrichtigung potenziell für jedes der anderen Gründe auftreten. Es wird jedoch nur einmal für jeden Grund auftreten. Nachdem die Benachrichtigung für jeden Grund einmal aufgetreten ist, erhalten Sie eine Benachrichtigung nur für das Hinzufügen eines neuen Datensatzes.  
  
 Im Gegensatz dazu müssen Sie festlegen *AdStatus* auf **AdStatusUnwantedEvent** nur einmal an, die Anforderung einen Ereignishandler, ohne eine **AdReason** empfangenden Parameter Stop-Ereignis Benachrichtigungen werden gesendet.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-Ereignisinstanziierung nach Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Zusammenwirken der Ereignishandler](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Typen von Ereignissen](../../../ado/guide/data/types-of-events.md)
