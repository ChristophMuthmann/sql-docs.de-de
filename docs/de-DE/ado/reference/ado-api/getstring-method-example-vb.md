---
title: GetString-Methode (Beispiel) (VB) | Microsoft Docs
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
dev_langs:
- VB
helpviewer_keywords:
- GetString method [ADO], Visual Basic example
ms.assetid: 14c96d71-46a8-4782-b474-80ce348e8bff
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbec3ed2a2bba52f3a1757867c3e30e0cb8204cb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getstring-method-example-vb"></a>GetString-Methode (Beispiel) (VB)
Dieses Beispiel zeigt die [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) Methode.  
  
 Angenommen, Sie Debuggen eine Zugriffsproblems, das Daten und eine schnelle und einfache Möglichkeit zum Drucken des aktuellen Inhalts eine kleine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
```  
'BeginGetStringVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
    Dim varOutput As Variant  
  
     ' specific variables  
    Dim strPrompt As String  
    Dim strState As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' get user input  
    strPrompt = "Enter a state (CA, IN, KS, MD, MI, OR, TN, UT): "  
    strState = Trim(InputBox(strPrompt, "GetString Example"))  
  
     ' open recordset  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_fname, au_lname, address, city FROM Authors " & _  
                "WHERE state = '" & strState & "'"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    If Not rstAuthors.EOF Then  
    ' Use all defaults: get all rows, TAB as column delimiter,  
    ' CARRIAGE RETURN as row delimiter, EMPTY-string as null delimiter  
       varOutput = rstAuthors.GetString(adClipString)  
        ' print output  
       Debug.Print "State = '" & strState & "'"  
       Debug.Print "Name             Address             City" & vbCr  
       Debug.Print varOutput  
    Else  
       Debug.Print "No rows found for state = '" & strState & "'" & vbCr  
    End If  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndGetStringVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GetString-Methode (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
