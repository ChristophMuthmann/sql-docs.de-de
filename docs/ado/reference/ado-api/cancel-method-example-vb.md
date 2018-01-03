---
title: Cancel-Methode (Beispiel) (VB) | Microsoft Docs
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
dev_langs: VB
helpviewer_keywords: Cancel method [ADO], Visual Basic example
ms.assetid: 5c0530ad-68d0-4cba-b1af-9386d566c7c5
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7d275baef72033521f0ad85a4337aac3dd624ad
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="cancel-method-example-vb"></a>Cancel-Methode (Beispiel) (VB)
Dieses Beispiel verwendet die ["Abbrechen"](../../../ado/reference/ado-api/cancel-method-ado.md) Methode zum Abbrechen der Ausführung einer Befehls auf einen [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt, wenn die Verbindung ausgelastet ist.  
  
```  
'BeginCancelVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strCmdChange As String  
    Dim strCmdRestore As String  
     'record variables  
    Dim blnChanged As Boolean  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Define command strings  
    strCmdChange = "UPDATE titles SET type = 'self_help' WHERE type = 'psychology'"  
    strCmdRestore = "UPDATE titles SET type = 'psychology' " & _  
                     "WHERE type = 'self_help'"  
  
    ' Begin a transaction, then execute a command asynchronously  
    Cnxn.BeginTrans  
    Cnxn.Execute strCmdChange, , adAsyncExecute  
    ' do something else for a little while –  
    ' use i = 1 to 32000 to allow completion  
    Dim i As Integer  
    For i = 1 To 1000  
        i = i + i  
        Debug.Print i  
    Next i  
  
    ' If the command has NOT completed, cancel the execute and  
    ' roll back the transaction; otherwise, commit the transaction  
    If CBool(Cnxn.State And adStateExecuting) Then  
        Cnxn.Cancel  
        Cnxn.RollbackTrans  
        blnChanged = False  
        MsgBox "Update canceled."  
    Else  
        Cnxn.CommitTrans  
        blnChanged = True  
        MsgBox "Update complete."  
    End If  
  
    ' If the change was made, restore the data  
    ' because this is only a demo  
    If blnChanged Then  
        Cnxn.Execute strCmdRestore  
        MsgBox "Data restored."  
    End If  
  
    ' clean up  
    Cnxn.Close  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCancelVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Cancel-Methode (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
