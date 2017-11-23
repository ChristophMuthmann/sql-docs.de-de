---
title: "Erkennen und Lösen von Konflikten | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ac1ca3e4cd6e9047f6a3f47e8067efc6143ba5a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="detecting-and-resolving-conflicts"></a>Erkennen und Lösen von Konflikten
Wenn Sie das Recordset in unmittelbarer Modus arbeiten, ist wesentlich weniger fehleranfällig für Parallelitätsprobleme auftreten. Andererseits, wenn Ihre Anwendung BatchUpdates Modus verwendet, liegt möglicherweise eine gute chance, dass ein Benutzer ändert einen Datensatz, vor dem Speichern von Änderungen, die von einem anderen Benutzer, die den gleichen Datensatz bearbeiten vorgenommen wurden. In diesem Fall sollten Sie die Anwendung den Konflikt Datenbindungsvorgängen erfolgreich behandelt. Sie können Ihr Wunsch sein, die letzte Person, die ein Update an den Server senden "gewinnt". Oder Sie können die letzten Benutzer, um zu entscheiden, welche Vorrang haben soll, indem ihm mithilfe einer Auswahl zwischen den beiden in Konflikt stehenden Werten bereitstellen möchten.  
  
 In jedem Fall stellt ADO die OriginalValue und OriginalValue Eigenschaften der Field-Objekt, um diese Art von Konflikten zu behandeln. Verwenden Sie diese Eigenschaften in Kombination mit dem Resync-Methode und die Filter-Eigenschaft des Recordset-Objekts.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ADO während einer Batchaktualisierung einen Konflikt auftritt, wird der fehlerauflistung eine Warnung hinzugefügt. Aus diesem Grund sollten Sie immer auf Fehler überprüfen, sofort nach dem BatchUpdate aufrufen, und wenn werden gefunden dem Testen der Annahme, dass Sie ein Konflikt festgestellt haben. Der erste Schritt ist die Filter-Eigenschaft auf das Recordset gleich vorliegt festgelegt. Dies schränkt die Sicht auf Ihre Recordset, um nur die Datensätze, die miteinander in Konflikt stehen. Die RecordCount-Eigenschaft ungleich 0 (null), nach diesem Schritt ist, wissen Sie, dass etwas anderes als ein Konflikt ausgelöst wurde.  
  
 Wenn Sie BatchUpdate aufrufen, ADO und der Anbieter SQL-Anweisungen zum Durchführen von Updates in der Datenquelle generieren. Denken Sie daran, dass bestimmte Datenquellen Beschränkungen gelten für die Datentypen der Spalten in einer WHERE-Klausel verwendet werden können.  
  
 Rufen Sie als Nächstes die Resync-Methode auf das Recordset mit vom Argument AffectRecords AdAffectGroup und vom ResyncValues Argument AdResyncUnderlyingValues gleich. Die Resync-Methode aktualisiert die Daten in den aktuellen Recordset-Objekt aus der zugrunde liegenden Datenbank. Mithilfe von AdAffectGroup stellen Sie sicher, dass nur die Datensätze, die mit dem aktuellen Filter festlegen, d. h. nur die in Konflikt stehende Datensätze angezeigt mit der Datenbank synchronisiert werden. Dies womöglich einen deutlichen Unterschied, wenn Sie mit einem großen Recordset arbeiten. Durch das ResyncValues-Argument auf AdResyncUnderlyingValues festlegen, wenn Resync aufrufen, stellen Sie sicher, dass die OriginalValue-Eigenschaft den Wert (Konflikt), aus der Datenbank enthalten, die Value-Eigenschaft den vom Benutzer eingegebenen Wert beibehält und dass die OriginalValue-Eigenschaft den ursprünglichen Wert für das Feld (der Wert, der vor der letzten erfolgreichen UpdateBatch Puffermethode wurde) gespeichert werden. Sie können diese Werte dann verwenden, lösen Sie den Konflikt programmgesteuert oder muss der Benutzer den Wert auswählen, der verwendet werden.  
  
 Diese Technik wird im folgenden Codebeispiel wird angezeigt. Das Beispiel erstellt einen Konflikt künstlich mithilfe eines separaten Recordsets einen Wert in der zugrunde liegenden Tabelle ändern, bevor UpdateBatch aufgerufen wird.  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 Sie können die Status-Eigenschaft des aktuellen Datensatzes oder eines bestimmten Felds verwenden, um zu bestimmen, welche Art von Konflikt aufgetreten ist.  
  
 Ausführliche Informationen zur Fehlerbehandlung finden Sie unter [Fehlerbehandlung](../../../ado/guide/data/error-handling.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Batchmodus](../../../ado/guide/data/batch-mode.md)
