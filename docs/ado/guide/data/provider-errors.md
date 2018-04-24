---
title: Anbieterfehler | Microsoft Docs
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
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 14f79d299850bf6163fb328b0dd54be9d84f9a7b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="provider-errors"></a>Anbieterfehler
Wenn ein Anbieterfehler auftritt, wird ein Laufzeitfehler-2147467259 zurückgegeben. Wenn Sie diesen Fehler erhalten, überprüfen Sie die **Fehler** Auflistung der aktiven **Verbindung** -Objekt, das enthält einen oder mehrere Fehler, die beschreiben, was aufgetreten ist.  
  
## <a name="the-ado-errors-collection"></a>Die Auflistung der ADO-Fehler  
 ADO verfügbar macht eine Auflistung von Fehlerobjekte über da ADO-Vorgang mehrere Anbieterfehler erzeugen kann, die **Verbindung** Objekt. Diese Sammlung enthält keine Objekte aus, wenn ein Vorgang wird erfolgreich abgeschlossen, und ein oder mehrere enthält **Fehler** Objekten zurück, wenn Fehler aufgetreten, und der Anbieter wird mindestens ein Fehler ausgelöst. Untersuchen Sie jeden Error-Objekt, um die genaue Ursache des Fehlers zu bestimmen.  
  
 Sobald Sie die Behandlung von Fehler haben abgeschlossen haben, können Sie die Auflistung deaktivieren, durch Aufrufen der **deaktivieren** Methode. Es ist besonders wichtig, deaktivieren Sie explizit die **Fehler** Auflistung vor dem Aufruf der **Resync**, **UpdateBatch**, oder **CancelBatch**Methode auf eine **Recordset** -Objekt, der **öffnen** Methode auf eine **Verbindung** -Objekt, oder legen Sie die **Filter** Eigenschaft auf einen **Recordset** Objekt. Durch die Auflistung explizit deaktivieren, werden Sie sicher, dass alle **Fehler** Objekte in der Auflistung nicht von einem früheren Vorgang übrig sind.  
  
 Einige Vorgänge können zusätzlich zu Fehlern Warnungen generieren. Warnungen werden auch durch dargestellt **Fehler** Objekte in der **Fehler** Auflistung. Wenn ein Anbieter eine Warnung zur Auflistung hinzufügt, wird es kein Laufzeitfehler generiert. Überprüfen Sie die **Anzahl** Eigenschaft von der **Fehler** -Auflistung, um zu bestimmen, ob eine Warnung von einem bestimmten Vorgang erstellt wurde. Sofern die Anzahl die oder größer ist, ein **Fehler** Objekt wurde der Auflistung hinzugefügt. Sobald Sie, dass festgestellt haben die **Fehler** Auflistung enthält, Fehler oder Warnungen, können Sie die Auflistung durchlaufen und Abrufen von Informationen zu den einzelnen **Fehler** -Objekt, das sie enthält. Die folgende kurze Visual Basic-Beispiel veranschaulicht dies:  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 Die Fehlerbehandlung Routine enthält eine **für jede** Schleife, in der jedes Objekt in untersucht die **Fehler** Auflistung. In diesem Beispiel wird erfasst eine Nachricht für die Anzeige. In einem Programm arbeiten, Schreiben Sie Code zum Durchführen von eines entsprechenden Tasks für jeden Fehler, z. B. das schließen alle Dateien öffnen und das Programm systematisch heruntergefahren.  
  
## <a name="the-error-object"></a>Die Error-Objekt  
 Mithilfe einer **Fehler** -Objekts können Sie bestimmen, welche Fehler aufgetreten ist und noch wichtiger ist, welche Anwendung oder welches Objekt den Fehler verursacht hat. Die **Fehler** Objekt hat die folgenden Eigenschaften:  
  
|Eigenschaftsname|Description|  
|-------------------|-----------------|  
|**Beschreibung**|Eine textbeschreibung des Fehlers, der aufgetreten ist.|  
|**HelpContext HelpFile**|Bezieht sich auf das Hilfethema und Hilfe-Datei, die eine Beschreibung des Fehlers enthalten, die aufgetreten sind.|  
|**NativeError**|Die anbieterspezifische Fehlernummer.|  
|**Anzahl**|Ein Long Integer-Wert, der die Anzahl darstellt (aufgeführt der **ErrorValueEnum**) des aufgetretenen Fehlers.|  
|**Quelle**|Gibt den Namen des Objekts oder der Anwendung, die ein Fehler generiert.|  
|**SQLState**|Eine fünfstellige Fehlercode, den der Anbieter während des Prozesses, der eine SQL-Anweisung zurückgibt.|  
  
 Das ADO **Fehler** Objekt ähnelt stark der standardmäßigen Visual Basic **Err** Objekt. Die Eigenschaften beschreiben aufgetretenen Fehlers. Zusätzlich zur Anzahl der Fehler erhalten Sie auch zwei verwandte Angaben. Die **NativeError** Eigenschaft enthält die Fehlernummer spezifisch für den Datenanbieter Sie verwenden. Im vorherigen Beispiel ist der Anbieter Microsoft OLE DB-Anbieter für SQL Server, daher **NativeError** enthält Fehler, die spezifisch für SQL Server. Die **SQLState** Eigenschaft verfügt über eine fünfstellige-Code, der ein Fehler in einer SQL­Anweisung beschrieben wird.  
  
## <a name="event-related-errors"></a>Fehler im Zusammenhang mit Ereignis  
 Die **Fehler** Objekt wird auch verwendet, wenn ereignisbezogene Fehler auftreten. Sie können bestimmen, ob im Prozess ist ein Fehler, die ein ADO-Ereignis ausgelöst wird aufgetreten, indem Sie überprüfen die **Fehler** Objekt als Ereignisparameter übergeben.  
  
 Wenn der Vorgang, der bewirkt, ein Ereignis dass erfolgreich abgeschlossen wird der *AdStatus* Parameter des ereignishandlers festgelegt *AdStatusOK*. Andererseits, wenn der Vorgang, der das Ereignis ausgelöst wurde nicht erfolgreich war, die *AdStatus* Parametersatz auf *AdStatusErrorsOccurred*. In diesem Fall die *pError* Parameter enthält einen **Fehler** -Objekt, das den Fehler beschreibt.
