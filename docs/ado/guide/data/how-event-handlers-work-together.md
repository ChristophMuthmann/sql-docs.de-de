---
title: Zusammenwirken der Ereignishandler | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a2e603819e2d4c44bf612d62f86f448c560e0828
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="how-event-handlers-work-together"></a>Zusammenwirken der Ereignishandler
Es sei denn, Sie in Visual Basic wird für alle Ereignishandler programmieren **Verbindung** und **Recordset** Ereignisse implementiert werden müssen, unabhängig davon, ob Sie tatsächlich alle Ereignisse verarbeiten. Der Arbeitsaufwand, der Implementierung müssen Sie lediglich hängt von der Programmiersprache ab. Weitere Informationen finden Sie unter [ADO Ereignisinstanziierung von Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Kombiniertes Ereignis-Handler  
 Jeder Ereignishandler wird, verfügt über eine zugeordnete **Complete** -Ereignishandler. Z. B. wenn die Anwendung ändert den Wert eines Felds, das **WillChangeField** Ereignishandler wird aufgerufen. Wenn die Änderung zulässig ist, bleibt die **AdStatus** Parameter unverändert, und der Vorgang ausgeführt wird. Wenn der Vorgang abgeschlossen ist, eine **FieldChangeComplete** Ereignis benachrichtigt die Anwendung, die der Vorgang abgeschlossen wurde. Wenn er erfolgreich abgeschlossen **AdStatus** enthält **AdStatusOK**ist, andernfalls **AdStatus** enthält **AdStatusErrorsOccurred** und Sie müssen überprüfen, die **Fehler** Objekt, das die Ursache des Fehlers zu ermitteln.  
  
 Wenn **WillChangeField** wird aufgerufen, Sie möglicherweise feststellen, dass die Änderung nicht vorgenommen werden soll. In diesem Fall legen **AdStatus** auf **AdStatusCancel.** Der Vorgang abgebrochen und die **FieldChangeComplete** -Ereignis empfängt ein **AdStatus** Wert **AdStatusErrorsOccurred**. Die **Fehler** Objekt enthält **AdErrOperationCancelled** , damit Ihre **FieldChangeComplete** Handler weiß, dass der Vorgang abgebrochen wurde. Allerdings müssen Sie den Wert der Überprüfen der **AdStatus** Parameter vor dem ändern, da das Festlegen **AdStatus** auf **AdStatusCancel** hat keine Auswirkung, wenn der Parameter festgelegt wurde um **AdStatusCantDeny** beim Einstieg in die Prozedur.  
  
 In einigen Fällen kann ein Vorgang mehr als ein Ereignis auslösen. Z. B. die **Recordset** Objekt verfügt über Ereignisse für gekoppelt **Feld** Änderungen und **Datensatz** ändert. Wenn die Anwendung ändert den Wert von einer **Feld**, die **WillChangeField** Ereignishandler wird aufgerufen. Wenn es feststellt, dass der Vorgang fortgesetzt werden kann, die **WillChangeRecord** -Ereignishandler wird auch ausgelöst. Wenn dieser Handler auch das Ereignis, um den Vorgang fortzusetzen kann, die Änderung vorgenommen wird und die **FieldChangeComplete** und **RecordChangeComplete** -Ereignishandler werden aufgerufen. Die Reihenfolge, in der der Ereignishandler wird für einen bestimmten Vorgang aufgerufen werden, ist nicht definiert, daher Sie vermeiden sollten, Schreiben von Code, die davon abhängen Ereignishandler in einer bestimmten Reihenfolge aufgerufen.  
  
 Wenn mehrere werden Ereignisse ausgelöst werden, kann eines der Ereignisse in Instanzen den ausstehenden Vorgang abbrechen. Z. B. wenn die Anwendung ändert den Wert von einer **Feld**, beide **WillChangeField** und **WillChangeRecord** würde normalerweise-Ereignishandler aufgerufen werden. Jedoch, wenn der Vorgang, in der ersten Ereignishandler, die zugehörigen abgebrochen wird **abgeschlossen** Handler wird sofort aufgerufen, mit **AdStatusOperationCancelled**. Der zweite Handler wird nie aufgerufen. Wenn jedoch der erste Ereignishandler das Ereignis zu fortfahren kann, wird der andere Ereignishandler aufgerufen werden. Wenn sie dann den Vorgang abbricht beide **Complete** Ereignisse werden aufgerufen, wie in den früheren Beispielen.  
  
## <a name="unpaired-event-handlers"></a>Nicht zugeordnete Ereignis-Handler  
 Solange der Status zu übergeben ist das Ereignis nicht **AdStatusCantDeny**, ereignisbenachrichtigungen für jedes Ereignis deaktivieren, wird durch zurückgeben **AdStatusUnwantedEvent** in den *Status*Parameter. Beispielsweise, wenn Ihre **Complete** Ereignishandler erstmalig aufgerufen wird, können Sie zurückkehren, **AdStatusUnwantedEvent**. Sie erhalten anschließend nur **wird** Ereignisse. Einige Ereignisse können jedoch mehrere Gründen ausgelöst werden. In diesem Fall hat das Ereignis ein *Grund* Parameter. Wenn Sie zurückkehren **AdStatusUnwantedEvent**, hält Sie empfangen von Benachrichtigungen für dieses Ereignis nur, wenn sie für diesen bestimmten Grund auftreten. Das heißt, erhalten potenziell Benachrichtigung für jede mögliche Ursache Sie, dass das Ereignis ausgelöst werden konnte.  
  
 Einzelne **wird** Ereignishandler können nützlich sein, wenn die Parameter zu überprüfen, die in einem Vorgang verwendet werden sollen. Sie können diese Vorgangsparameter ändern oder brechen Sie den Vorgang.  
  
 Lassen Sie alternativ **Complete** ereignisbenachrichtigung aktiviert. Wenn der Ereignishandler für das erste wird aufgerufen wird, zurückgeben **AdStatusUnwantedEvent**. Sie erhalten anschließend nur **Complete** Ereignisse.  
  
 Einzelne **Complete** Ereignishandler können zum Verwalten von asynchronen Vorgängen nützlich sein. Jeder asynchronen Vorgang hat eine entsprechende **Complete** Ereignis.  
  
 Beispielsweise können dauert sehr lange zum Auffüllen eines großen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Wenn die Anwendung richtig geschrieben ist, können Sie starten einen `Recordset.Open(...,adAsyncExecute)` Vorgang und fahren Sie mit anderen Verarbeitungsschritten. Schließlich werden benachrichtigt, wenn die **Recordset** werden ausgefüllt, indem ein **ExecuteComplete** Ereignis.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Einzelne Ereignishandler und mehrere Objekte  
 Die Flexibilität einer Programmiersprache wie Microsoft Visual C++® ermöglicht es Ihnen, eine Ereignis-Handler Verarbeitung von Ereignissen aus mehreren Objekten. Angenommen, Sie möglicherweise eine **trennen** Ereignishandler Verarbeitung von Ereignissen aus mehreren **Verbindung** Objekte. Wenn eine der Verbindungen beendet wurde, die **trennen** -Ereignishandler aufgerufen. Konnte Aufschluss darüber, welche Verbindung das Ereignis verursacht hat, da der Objektparameter Ereignishandler auf den entsprechenden festgelegt werden, würde **Verbindung** Objekt.  
  
> [!NOTE]
>  Diese Technik kann nicht in Visual Basic verwendet werden, weil diese Sprache nur ein Objekt mit einem Ereignishandler korreliert werden kann.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-Ereignisinstanziierung nach Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Ereignisparameter](../../../ado/guide/data/event-parameters.md)   
 [Typen von Ereignissen](../../../ado/guide/data/types-of-events.md)
