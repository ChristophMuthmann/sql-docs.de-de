---
title: Geben Sie die Beispiel-Eigenschaft (Feld) (VB) | Microsoft Docs
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
- Type property [field] [ADO], Visual Basic example
ms.assetid: accb72f5-a3bd-4a7e-92b6-6da0783b4b75
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ffbbc8356e1a53033b4c415d1ac6fa009a1e3f13
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="type-property-example-field-vb"></a>Beispiel für Eigenschaft (Feld) (VB)
In diesem Beispiel wird veranschaulicht, die [Typ](../../../ado/reference/ado-api/type-property-ado.md) durch Anzeigen der Namen der Konstanten entspricht, die auf den Wert der Eigenschaft der [Typ](../../../ado/reference/ado-api/type-property-ado.md) -Eigenschaft aller der [Feld](../../../ado/reference/ado-api/field-object.md) Objekte in der ***Mitarbeiter*** Tabelle. Die FieldType-Funktion ist erforderlich, damit dieses Verfahren ausführen.  
  
```  
'BeginTypeFieldVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim strCnxn As String  
    Dim strSQLEmployee As String  
    Dim FieldType As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset with data from Employees table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployee = "employee"  
    rstEmployees.Open strSQLEmployee, Cnxn, , , adCmdTable  
    'rstEmployees.Open strSQLEmployee, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
     ' the above two lines of code are identical  
  
    Debug.Print "Fields in Employees Table:" & vbCr  
  
    ' Enumerate Fields collection of Employees table  
    For Each fld In rstEmployees.Fields  
        ' translate field-type code to text  
        Select Case fld.Type  
            Case adChar  
               FieldType = "adChar"  
            Case adVarChar  
               FieldType = "adVarChar"  
            Case adSmallInt  
               FieldType = "adSmallInt"  
            Case adUnsignedTinyInt  
               FieldType = "adUnsignedTinyInt"  
            Case adDBTimeStamp  
               FieldType = "adDBTimeStamp"  
        End Select  
        ' show results  
        Debug.Print "  Name: " & fld.Name & vbCr & _  
          "  Type: " & FieldType & vbCr  
    Next fld  
  
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
  
    Set fld = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndTypeFieldVB  
  
Attribute VB_Name = "TypeField"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)   
 [Type-Eigenschaft (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
