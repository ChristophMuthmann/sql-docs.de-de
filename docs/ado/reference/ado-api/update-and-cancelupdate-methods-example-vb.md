---
title: Update- und CancelUpdate Methoden Beispiel (VB) | Microsoft Docs
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
dev_langs:
- VB
helpviewer_keywords:
- CancelUpdate method [ADO]
- Update method [ADO], Visual Basic example
ms.assetid: 55bedd08-7440-4da4-b854-4ac9ef2fdedb
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c2f4f3de2ca297fb803eef8fd855611bf835282
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="update-and-cancelupdate-methods-example-vb"></a>Update- und CancelUpdate Methoden Beispiel (VB)
Dieses Beispiel zeigt die [Update](../../../ado/reference/ado-api/update-method.md) Methode in Verbindung mit der [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode.  
  
```  
'BeginUpdateVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' recordset and connection variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLEmployees As String  
     ' buffer variables  
    Dim strOldFirst As String  
    Dim strOldLast As String  
    Dim strMessage As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset to enable changes  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "SELECT fname, lname FROM Employee ORDER BY lname"  
    rstEmployees.Open strSQLEmployees, Cnxn, adOpenKeyset, adLockOptimistic, adCmdText  
  
    ' Store original data  
    strOldFirst = rstEmployees!fname  
    strOldLast = rstEmployees!lname  
    ' Change data in edit buffer  
    rstEmployees!fname = "Linda"  
    rstEmployees!lname = "Kobara"  
  
    ' Show contents of buffer and get user input  
    strMessage = "Edit in progress:" & vbCr & _  
        "  Original data = " & strOldFirst & " " & _  
        strOldLast & vbCr & "  Data in buffer = " & _  
        rstEmployees!fname & " " & rstEmployees!lname & vbCr & vbCr & _  
        "Use Update to replace the original data with " & _  
        "the buffered data in the Recordset?"  
  
    If MsgBox(strMessage, vbYesNo) = vbYes Then  
        rstEmployees.Update  
    Else  
        rstEmployees.CancelUpdate  
    End If  
  
    ' show the resulting data  
    MsgBox "Data in recordset = " & rstEmployees!fname & " " & _  
       rstEmployees!lname  
  
    ' restore original data because this is a demonstration  
    If Not (strOldFirst = rstEmployees!fname And _  
           strOldLast = rstEmployees!lname) Then  
        rstEmployees!fname = strOldFirst  
        rstEmployees!lname = strOldLast  
        rstEmployees.Update  
    End If  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndUpdateVB  
```  
  
 Dieses Beispiel zeigt die **Update** Methode in Verbindung mit der [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) Methode.  
  
```  
Attribute VB_Name = "Update"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Update-Methode](../../../ado/reference/ado-api/update-method.md)
