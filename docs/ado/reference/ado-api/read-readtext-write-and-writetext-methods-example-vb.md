---
title: Lesen, ReadText, schreiben und WriteText-Methoden-Beispiel (VB) | Microsoft Docs
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
- ReadText method [ADO], Visual Basic example
- Write method [ADO], Visual Basic example
- Read method [ADO], Visual Basic example
- WriteText method [ADO], Visual Basic example
ms.assetid: 699b73f7-04f9-4d46-94b2-6cb12be6de56
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c51ca097f3c1a9c71dbd75d00f7411b6dd61d03b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="read-readtext-write-and-writetext-methods-example-vb"></a>Lesen, ReadText, schreiben und WriteText-Methoden-Beispiel (VB)
In diesem Beispiel wird veranschaulicht, wie der Inhalt eines Textfelds in beide einen Text zu lesen [Stream](../../../ado/reference/ado-api/stream-object-ado.md) und eine binäre **Stream**. Einschließen von anderen Eigenschaften und Methoden gezeigt [Position](../../../ado/reference/ado-api/position-property-ado.md), [Größe](../../../ado/reference/ado-api/size-property-ado-parameter.md), [Charset](../../../ado/reference/ado-api/charset-property-ado.md), und [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
```  
'BeginReadVB  
Private Sub cmdRead_Click()  
    On Error GoTo ErrorHandler  
  
    'Declare variables  
    Dim objStream As Stream  
    Dim varA As Variant  
    Dim bytA() As Byte  
    Dim i As Integer  
    Dim strBytes As String  
  
    'Instantiate and Open Stream  
    Set objStream = New Stream  
    objStream.Open  
  
    'Write the text content of a textbox to the stream  
    If Text1.Text = "" Then  
        Err.Raise 1, , "The text field is blank."  
    End If  
    objStream.WriteText Text1.Text  
  
    'Display the text contents and size of the stream  
    objStream.Position = 0  
    Debug.Print "Default text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch character set and display  
    objStream.Position = 0  
    objStream.Charset = "Windows-1252"  
    Debug.Print "New Charset text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch to a binary stream and display  
    objStream.Position = 0  
    objStream.Type = adTypeBinary  
    Debug.Print "Binary:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Load an array of bytes with the text box text  
    ReDim bytA(Len(Text1.Text))  
    For i = 1 To Len(Text1.Text)  
        bytA(i - 1) = CByte(Asc(Mid(Text1.Text, i, 1)))  
    Next  
  
    'Write the buffer to the binary stream and display  
    objStream.Position = 0  
    objStream.Write bytA()  
    objStream.SetEOS  
    objStream.Position = 0  
    Debug.Print "Binary after Write:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Switch back to a text stream and display  
    Debug.Print "Translated back:"  
    objStream.Position = 0  
    objStream.Type = adTypeText  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    ' clean up  
    objStream.Close  
    Set objStream = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not objStream Is Nothing Then  
        If objStream.State = adStateOpen Then objStream.Close  
    End If  
    Set objStream = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndReadVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Charset-Eigenschaft (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)   
 [Positionseigenschaft (ADO)](../../../ado/reference/ado-api/position-property-ado.md)   
 [Read-Methode](../../../ado/reference/ado-api/read-method.md)   
 [ReadText-Methode](../../../ado/reference/ado-api/readtext-method.md)   
 [SetEOS-Methode](../../../ado/reference/ado-api/seteos-method.md)   
 [Eigenschaft "Größe" (ADO-Datenstrom)](../../../ado/reference/ado-api/size-property-ado-stream.md)   
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Write-Methode](../../../ado/reference/ado-api/write-method.md)   
 [WriteText-Methode](../../../ado/reference/ado-api/writetext-method.md)
