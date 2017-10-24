---
title: "Fehler-Objekt für Eigenschaften Beispiel (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Number property [ADO], Visual Basic example
- Source property [ADO], Visual Basic example
- NativeError property [ADO], Visual Basic example
- Description property [ADO], Visual Basic example
- HelpFile property [ADO], Visual Basic example
- SQLState property [ADO], Visual Basic example
- HelpContext property [ADO], Visual Basic example
ms.assetid: 5c728458-d85c-497c-afcf-2cfa36c3342a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 43385a04975c36109c420d3137c205bd184b121f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)
In diesem Beispiel löst einen Fehler aus, es aufgefangen und zeigt die [Beschreibung](../../../ado/reference/ado-api/description-property.md), [HelpContext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md), [HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md), [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md), [ Anzahl](../../../ado/reference/ado-api/number-property-ado.md), [Quelle](../../../ado/reference/ado-api/source-property-ado-error.md), und [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) Eigenschaften des resultierenden [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt.  
  
```  
'BeginDescriptionVB  
Public Sub Main()  
  
    Dim Cnxn As ADODB.Connection  
    Dim Err As ADODB.Error  
    Dim strError As String  
  
    On Error GoTo ErrorHandler  
  
    ' Intentionally trigger an error  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open "nothing"  
  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
  
    ' Enumerate Errors collection and display  
    ' properties of each Error object  
    For Each Err In Cnxn.Errors  
        strError = "Error #" & Err.Number & vbCr & _  
            "   " & Err.Description & vbCr & _  
            "   (Source: " & Err.Source & ")" & vbCr & _  
            "   (SQL State: " & Err.SQLState & ")" & vbCr & _  
            "   (NativeError: " & Err.NativeError & ")" & vbCr  
        If Err.HelpFile = "" Then  
            strError = strError & "   No Help file available"  
        Else  
            strError = strError & _  
               "   (HelpFile: " & Err.HelpFile & ")" & vbCr & _  
               "   (HelpContext: " & Err.HelpContext & ")" & _  
               vbCr & vbCr  
        End If  
  
        Debug.Print strError  
    Next  
  
    Resume Next  
End Sub  
'EndDescriptionVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Description-Eigenschaft](../../../ado/reference/ado-api/description-property.md)   
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)   
 [HelpContext HelpFile-Eigenschaften](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpContext HelpFile-Eigenschaften](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [NativeError-Eigenschaft (ADO)](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number-Eigenschaft (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source-Eigenschaft (ADO-Fehler)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState-Eigenschaft](../../../ado/reference/ado-api/sqlstate-property.md)

