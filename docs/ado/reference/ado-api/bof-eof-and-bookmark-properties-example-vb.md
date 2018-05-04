---
title: BOF, EOF und Lesezeichen-Eigenschaften-Beispiel (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- BOF property [ADO], Visual Basic example
- Bookmark property [ADO], Visual Basic example
- EOF property [ADO], Visual Basic example
ms.assetid: b6573c6e-fee8-4267-a722-fadaec6eafe6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d79be2676d2679fff103cfe9201e379e2d67033
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bof-eof-and-bookmark-properties-example-vb"></a>BOF, EOF und Lesezeichen-Eigenschaften-Beispiel (VB)
Dieses Beispiel verwendet die [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) und [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) eine Meldung angezeigt, wenn ein Benutzer versucht, verschieben Sie nach der ersten oder letzten Datensatz mit den Eigenschaften einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Verwendet die [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md) Eigenschaft der Benutzer einen Datensatz in ein flag einer **Recordset** und später zu ihr zurückkehren.  
  
```  
'BeginBOFVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstPublishers As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLPubs As String  
     'record variables  
    Dim strMessage As String  
    Dim intCommand As Integer  
    Dim varBookmark As Variant  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' Open recordset and use client cursor  
     ' to enable AbsolutePosition property  
    Set rstPublishers = New ADODB.Recordset  
    strSQLPubs = "SELECT pub_id, pub_name FROM publishers ORDER BY pub_name"  
    rstPublishers.Open strSQLPubs, strCnxn, adUseClient, adOpenStatic, adCmdText  
  
    rstPublishers.MoveFirst  
    Do Until rstPublishers.EOF  
        ' Display information about current record  
        ' and get user input  
        strMessage = "Publisher: " & rstPublishers!pub_name & _  
            vbCr & "(record " & rstPublishers.AbsolutePosition & _  
            " of " & rstPublishers.RecordCount & ")" & vbCr & vbCr & _  
            "Enter command:" & vbCr & _  
            "[1 - next / 2 - previous /" & vbCr & _  
            "3 - set bookmark / 4 - go to bookmark]"  
        intCommand = Val(InputBox(strMessage))  
  
        ' Check user input  
        Select Case intCommand  
            Case 1  
                ' Move forward trapping for EOF  
                rstPublishers.MoveNext  
                If rstPublishers.EOF Then  
                    MsgBox "Moving past the last record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveLast  
                End If  
            Case 2  
                ' Move backward trapping for BOF  
                rstPublishers.MovePrevious  
                If rstPublishers.BOF Then  
                    MsgBox "Moving past the first record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveFirst  
                End If  
            Case 3  
                ' Store the bookmark of the current record  
                varBookmark = rstPublishers.Bookmark  
            Case 4  
                ' Go to the record indicated by the stored bookmark  
                If IsEmpty(varBookmark) Then  
                    MsgBox "No Bookmark set!"  
                Else  
                    rstPublishers.Bookmark = varBookmark  
                End If  
            Case Else  
                Exit Do  
        End Select  
    Loop  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndBOFVB  
```  
  
 Dieses Beispiel verwendet die **Lesezeichen** und [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaften eine eingeschränkte Ansicht der Erstellung der **Recordset**. Nur Datensätze verweist auf das Array von Lesezeichen werden zugegriffen.  
  
```  
Attribute VB_Name = "BOF"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BOF, EOF-Eigenschaften (ADO)](../../../ado/reference/ado-api/bof-eof-properties-ado.md)   
 [Bookmark-Eigenschaft (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
