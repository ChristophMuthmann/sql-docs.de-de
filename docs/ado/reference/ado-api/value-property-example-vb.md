---
title: "Beispiel für Dateneigenschaften (VB)-Wert | Microsoft Docs"
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
- Value property [ADO], Visual Basic example
ms.assetid: 2d4fe651-ef09-461b-8884-a70b6af4362e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2a17b5e2ee2f8f206ec924ae898d0bcb702a16f0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="value-property-example-vb"></a>Beispiel-Eigenschaft (VB)
Dieses Beispiel zeigt die [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft mit dem [Feld](../../../ado/reference/ado-api/field-object.md) und [Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md) Objekte anzeigen und die Eigenschaftswerte für die ***Mitarbeiter*** Tabelle.  
  
```  
'BeginValueVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' connection and recordset variables  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLEmployees As String  
     ' field property variables  
    Dim fld As ADODB.Field  
    Dim prp As ADODB.Property  
  
     ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset with data from Employees table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployees = "employee"  
    rstEmployees.Open strSQLEmployees, Cnxn, , , adCmdTable  
    'rstEmployees.Open strSQLEmployees, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
    ' the above two lines of code are identical  
  
    Debug.Print "Field values in rstEmployees"  
  
    ' Enumerate the Fields collection of the Employees table  
    For Each fld In rstEmployees.Fields  
        ' Because Value is the default property of a  
        ' Field object, the use of the actual keyword  
        ' here is optional.  
        Debug.Print "   " & fld.Name & " = " & fld.Value  
    Next fld  
  
    Debug.Print "Property values in rstEmployees"  
  
    ' Enumerate the Properties collection of the Recordset object  
    For Each prp In rstEmployees.Properties  
        Debug.Print "   " & prp.Name & " = " & prp.Value  
        ' because Value is the default property of a Property object  
        ' use of the actual Value keyword is optional  
    Next prp  
  
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
'EndValueVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)   
 [Property-Objekt (ADO)](../../../ado/reference/ado-api/property-object-ado.md)   
 [Value-Eigenschaft (ADO)](../../../ado/reference/ado-api/value-property-ado.md)

