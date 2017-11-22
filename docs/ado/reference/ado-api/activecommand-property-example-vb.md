---
title: "Beispiel für ActiveCommand-Eigenschaft (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords: ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc182bf90f130a351eabd3ce1cc0dd257cb93788
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="activecommand-property-example-vb"></a>Beispiel für ActiveCommand-Eigenschaft (VB)
Dieses Beispiel zeigt die [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md) Eigenschaft.  
  
 Eine Unterroutine erhält eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt, dessen **ActiveCommand** Eigenschaft dient zum Anzeigen der Befehlstext und die Parameter, die erstellt die **Recordset**.  
  
```  
'BeginActiveCommandVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
        'recordset and connection variables  
    Dim cmd As ADODB.Command  
    Dim rst As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
        'record variables  
    Dim strPrompt As String  
    Dim strName As String  
  
    Set Cnxn = New ADODB.Connection  
    Set cmd = New ADODB.Command  
  
    strPrompt = "Enter an author's name (e.g., Ringer): "  
    strName = Trim(InputBox(strPrompt, "ActiveCommandX Example"))  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
        'create SQL command string  
    cmd.CommandText = "SELECT * FROM Authors WHERE au_lname = ?"  
    cmd.Parameters.Append cmd.CreateParameter("LastName", adChar, adParamInput, 20, strName)  
  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
  
        'create the recordset by executing command string  
    Set rst = cmd.Execute(, , adCmdText)  
        'see the results  
    Call ActiveCommandXprint(rst)  
  
    ' clean up  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveCommandVB  
```  
  
 Die **ActiveCommandXprint** Routine erhält nur eine **Recordset** -Objekt noch Drucken muss der Befehlstext und die Parameter, die erstellt die **Recordset**. Dies kann erfolgen, da die **Recordset** des Objekts **ActiveCommand** Eigenschaft ergibt die zugeordnete [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt.  
  
 Die **Befehl** des Objekts [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft liefert den parametrisierten Befehl, der erstellt die **Recordset**. Die **Befehl** des Objekts [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung ergibt den Wert, der durch den Befehl Parameterplatzhalter ersetzt wurde ("**?**").  
  
 Schließlich werden Name und ID eine Fehlermeldung oder des Autors gedruckt.  
  
```  
'BeginActiveCommandPrintVB  
Public Sub ActiveCommandXprint(rstp As ADODB.Recordset)  
  
    Dim strName As String  
  
    strName = rstp.ActiveCommand.Parameters.Item("LastName").Value  
  
    Debug.Print "Command text = '"; rstp.ActiveCommand.CommandText; "'"  
    Debug.Print "Parameter = '"; strName; "'"  
  
    If rstp.BOF = True Then  
       Debug.Print "Name = '"; strName; "', not found."  
    Else  
       Debug.Print "Name = '"; rstp!au_fname; " "; rstp!au_lname; _  
             "', author ID = '"; rstp!au_id; "'"  
    End If  
  
    rstp.Close  
    Set rstp = Nothing  
End Sub  
'EndActiveCommandPrintVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveCommand-Eigenschaft (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
