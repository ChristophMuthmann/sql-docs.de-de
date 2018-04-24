---
title: AppendChunk und GetChunk Methoden Beispiel (VB) | Microsoft Docs
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
- GetChunk method [ADO], Visual Basic example
- AppendChunk method [ADO], Visual Basic example
ms.assetid: c07862b5-e466-46bd-910b-59ac96709cb9
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f807ed98872dcfc6d8b850108dbaced77dcbf7cb
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="appendchunk-and-getchunk-methods-example-vb"></a>AppendChunk und GetChunk Methoden Beispiel (VB)
Dieses Beispiel verwendet die [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) und [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) Methoden, um ein Bildfeld mit Daten aus einem anderen Datensatz zu füllen.  
  
```  
'BeginAppendChunkVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim rstPubInfo As ADODB.Recordset  
    Dim strSQLPubInfo As String  
     'record variables  
    Dim strPubID As String  
    Dim strPRInfo As String  
    Dim lngOffset As Long  
    Dim lngLogoSize As Long  
    Dim varLogo As Variant  
    Dim varChunk As Variant  
    Dim strMsg As String  
  
    Const conChunkSize = 100  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open the pub_info table with a cursor that allows updates  
    Set rstPubInfo = New ADODB.Recordset  
    strSQLPubInfo = "pub_info"  
    rstPubInfo.Open strSQLPubInfo, Cnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Prompt for a logo to copy  
    strMsg = "Available logos are : " & vbCr & vbCr  
    Do While Not rstPubInfo.EOF  
        strMsg = strMsg & rstPubInfo!pub_id & vbCr & _  
            Left(rstPubInfo!pr_info, InStr(rstPubInfo!pr_info, ",") - 1) & _  
            vbCr & vbCr  
        rstPubInfo.MoveNext  
    Loop  
  
    strMsg = strMsg & "Enter the ID of a logo to copy:"  
    strPubID = InputBox(strMsg)  
  
    ' Copy the logo to a variable in chunks  
    rstPubInfo.Filter = "pub_id = '" & strPubID & "'"  
    lngLogoSize = rstPubInfo!logo.ActualSize  
    Do While lngOffset < lngLogoSize  
        varChunk = rstPubInfo!logo.GetChunk(conChunkSize)  
        varLogo = varLogo & varChunk  
        lngOffset = lngOffset + conChunkSize  
    Loop  
  
    ' Get data from the user  
    strPubID = Trim(InputBox("Enter a new pub ID" & _  
                             " [must be > 9899 & < 9999]:"))  
  
    strPRInfo = Trim(InputBox("Enter descriptive text:"))  
  
    ' Add the new publisher to the publishers table to avoid  
    ' getting an error due to foreign key constraint  
    Cnxn.Execute "INSERT publishers(pub_id, pub_name) VALUES('" & _  
                   strPubID & "','Your Test Publisher')"  
  
    ' Add a new record, copying the logo in chunks  
    rstPubInfo.AddNew  
    rstPubInfo!pub_id = strPubID  
    rstPubInfo!pr_info = strPRInfo  
  
    lngOffset = 0 ' Reset offset  
    Do While lngOffset < lngLogoSize  
        varChunk = LeftB(RightB(varLogo, lngLogoSize - lngOffset), _  
            conChunkSize)  
        rstPubInfo!logo.AppendChunk varChunk  
        lngOffset = lngOffset + conChunkSize  
    Loop  
    rstPubInfo.Update  
  
    ' Show the newly added data  
    MsgBox "New record: " & rstPubInfo!pub_id & vbCr & _  
        "Description: " & rstPubInfo!pr_info & vbCr & _  
        "Logo size: " & rstPubInfo!logo.ActualSize  
  
    ' Delete new records because this is a demo  
    rstPubInfo.Requery  
    Cnxn.Execute "DELETE FROM pub_info " & _  
        "WHERE pub_id = '" & strPubID & "'"  
  
    Cnxn.Execute "DELETE FROM publishers " & _  
        "WHERE pub_id = '" & strPubID & "'"  
  
    ' clean up  
    rstPubInfo.Close  
    Cnxn.Close  
    Set rstPubInfo = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstPubInfo Is Nothing Then  
        If rstPubInfo.State = adStateOpen Then rstPubInfo.Close  
    End If  
    Set rstPubInfo = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndAppendChunkVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [AppendChunk-Methode (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)   
 [GetChunk-Methode (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)   
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)
