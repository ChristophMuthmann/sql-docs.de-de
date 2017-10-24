---
title: Bearbeiten von Daten | Microsoft Docs
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
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a5921185f6643f328559e3bc73dfac46bfee0c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="editing-data"></a>Bearbeiten von Daten
Wir haben erläutert wie ADO verwenden, um eine Verbindung mit einer Datenquelle herstellen, einen Befehl auszuführen, rufen Sie die Ergebnisse einem **Recordset** Objekt, und navigieren Sie in der **Recordset**. Dieser Abschnitt konzentriert sich auf den nächsten grundlegenden ADO-Vorgang: Bearbeiten von Daten.  
  
 In diesem Abschnitt verwenden Sie das Beispiel weiterhin **Recordset** hypervisorbasierte [Untersuchen von Daten](../../../ado/guide/data/examining-data.md), mit einer wichtigen Änderung. Der folgende Code dient zum Öffnen der **Recordset**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 Die wichtige Änderung des Codes besteht im Festlegen der **CursorLocation** Eigenschaft von der **Verbindung** Objekt gleich **AdUseClient** in der * GetNewConnection* Funktion (im nächsten Beispiel gezeigt), womit die Verwendung eines Client-Cursors. Weitere Informationen zu den Unterschieden zwischen Client- und serverseitigen Cursor finden Sie unter [Grundlegendes zu Cursorn und Sperren](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 Die **CursorLocation** der Eigenschaft **AdUseClient** Einstellung verschiebt die Position des Cursors aus der Datenquelle (in diesem Fall die SQL-Server) auf den Speicherort der Clientcode (der desktop-Arbeitsstation). Diese Einstellung erzwingt, dass ADO die Client-Cursormoduls für OLE DB-aufrufen, auf dem Client zum Erstellen und verwalten den Cursor.  
  
 Außerdem haben Sie gesehen, die die **LockType** Parameter von der **öffnen** Methode geändert werden, um **AdLockBatchOptimistic**. Daraufhin wird den Cursor im Batchmodus ausgeführt. (Der Anbieter speichert mehrere Änderungen und schreibt Sie sie in der zugrunde liegenden Datenquelle aus, nur bei Aufruf der **UpdateBatch** Methode.) Änderungen wurden an der **Recordset** wird nicht aktualisiert werden, in der Datenbank, bis der **UpdateBatch** Methode wird aufgerufen.  
  
 Schließlich verwendet der Code in diesem Abschnitt eine geänderte Version der GetNewConnection-Funktion. Diese Version der Funktion gibt jetzt einen clientseitigen Cursor zurück. Die Funktion sieht folgendermaßen aus:  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Bearbeiten vorhandener Einträge](../../../ado/guide/data/editing-existing-records.md)  
  
-   [Hinzufügen von Datensätzen](../../../ado/guide/data/adding-records.md)  
  
-   [Bestimmen, was unterstützt wird](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Löschen von Datensätzen, die mit der Delete-Methode](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [Alternativen: SQL-Anweisungen mithilfe](../../../ado/guide/data/alternatives-using-sql-statements.md)

