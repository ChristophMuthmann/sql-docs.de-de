---
title: ADO-Fehler | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7319f978370134775d7f89593716beac9fb73fab
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="ado-run-time-errors"></a>ADO-Laufzeitfehler
ADO-Fehler werden in Ihrem Programm als Laufzeitfehler gemeldet. Das Abfangen von Fehlern-Mechanismus von der Programmiersprache können zum Abfangen und behandeln. In Visual Basic verwenden, z. B. die **On Error** Anweisung. In Visual C++ hängt von der Methode, die Sie verwenden, um die ADO-Bibliotheken zugreifen. #Import verwenden eine **Try-Catch-** Block. Andernfalls müssen C++-Programmierer das Fehlerobjekt explizit durch den Aufruf abrufen **GetErrorInfo**. Die folgenden Visual Basic-Unterprozedur veranschaulicht Auffangen einen ADO-Fehler:

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 Dies **Form_Load** Ereignisprozedur absichtlich einen Fehler erstellt, indem versucht wird, öffnen Sie die gleiche **Verbindung** zweimal-Objekt. Ein zweites Mal die **öffnen** -Methode aufgerufen wird, der Fehlerhandler ist aktiviert. In diesem Fall wird der Fehler vom Typ **AdErrObjectOpen**, sodass der Fehlerhandler die folgende Meldung angezeigt wird, vor dem Fortsetzen der Ausführung des Programms:

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 Die Fehlermeldung enthält jede gebotenen Visual Basic Information **Err** Objekt, mit Ausnahme der **LastDLLError** -Wert, der hier nicht gilt. Die Nummer des Fehlers Aufschluss darüber, welche Fehler aufgetreten ist. Die Beschreibung ist hilfreich in Fällen, in denen Sie nicht den Fehler zu behandeln möchten. Sie können dabei einfach an den Benutzer übergeben. Obwohl Sie in der Regel Nachrichten angepasst, die für Ihre Anwendung verwenden möchten, können nicht alle Fehler zu erwarten sind; die Beschreibung gibt einen Hinweis, welcher Fehler vorliegt. Im Beispielcode wird der Fehler gemeldet wurde, durch die **Verbindung** Objekt. Sehen Sie das Objekt Typ oder ProgID hier – nicht auf einen Variablennamen ein.

> [!NOTE]
>  Visual Basic **Err** Objekt enthält nur Informationen zum letzten Fehler. Das ADO **Fehler** Auflistung von der **Verbindung** Objekt enthält ein **Fehler** Objekt für jeden Fehler, die von der letzten ADO-Vorgangs ausgelöst. Verwenden der **Fehler** Auflistung statt über das **Err** Objekt mehrere Fehler behandelt werden. Weitere Informationen zu den **Fehler** Auflistung finden Sie unter [Anbieterfehler](../../../ado/guide/data/provider-errors.md). Allerdings ist keine gültige **Verbindung** -Objekt, das **Err** Objekt ist die einzige Quelle für Informationen zur ADO-Fehler.

 Welche Arten von Vorgängen werden wahrscheinlich ADO-Fehler zu verursachen? Häufige ADO-Fehler können zwar öffnen ein Objekt wie z. B. eine **Verbindung** oder **Recordset**, bei dem Versuch, Daten aktualisieren oder Aufrufen einer Methode oder Eigenschaft, die von Ihrem Anbieter nicht unterstützt wird.

 OLE DB-Fehler können auch als Laufzeitfehler im an die Anwendung übergeben werden die **Fehler** Auflistung.

 Das folgende Thema enthält Informationen zum ADO-Fehler.

-   [ADO Error Reference (ADO-Fehlerreferenz)](../../../ado/guide/data/ado-error-reference.md)
