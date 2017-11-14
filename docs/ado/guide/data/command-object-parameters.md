---
title: Befehl Objektparameter | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Command object [ADO], parameters
ms.assetid: 10e7ef4a-78bf-4e91-931e-cbc6c065dd4c
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8eb9a6385a47030f5d9c9a283b56228ca68f596b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="command-object-parameters"></a>Befehlsobjekt-Parameter
Im vorherigen Thema erläutert [erstellen und Ausführen einer einfachen Befehl](../../../ado/guide/data/creating-and-executing-a-simple-command.md). Verwenden Sie eine weitere interessante für die [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt wird im nächsten Beispiel, in dem der SQL-Befehl parametrisiert wurde angezeigt. Diese Änderung ermöglicht den Befehl ein, und übergeben einen anderen Wert für den Parameter jedes Mal erneut verwenden. Da die [vorbereitet Eigenschaft](../../../ado/reference/ado-api/prepared-property-ado.md) Eigenschaft auf die **Befehl** -Objekts festgelegt wird, um **"true"**, ADO wird der Anbieter gezwungen, kompilieren Sie den Befehl, der im angegebenen [ CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) vor der ersten Ausführung. Es wird auch den kompilierte Befehl im Arbeitsspeicher beibehalten. Dies verlangsamt die Ausführung des Befehls etwas er, aufgrund des Mehraufwands ausgeführt wird für vorbereiten, jedoch führt zu einer Leistungssteigerung jedes Mal, wenn der Befehl, das anschließend aufgerufen wird zum ersten Mal. Aus diesem Grund sollten Befehle darauf vorbereitet sein, nur dann, wenn sie mehr als einmal verwendet werden sollen.  
  
```  
'BeginManualParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set the CommandText as a parameterized SQL query.  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = ? " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Prepare command because we will be executing it more than once.  
    objCmd.Prepared = True  
  
    ' Create new parameter for CustomerID. Initial value is ALFKI.  
    Set objParm1 = objCmd.CreateParameter("CustId", adChar, _  
                    adParamInput, 5, "ALFKI")  
    objCmd.Parameters.Append objParm1  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display.  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' .Set new param value, re-execute command, and display.  
    objCmd("CustId") = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndManualParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
 Nicht alle Anbieter unterstützen vorbereitete Befehle. Wenn befehlsvorbereitung von vom Anbieter nicht unterstützt werden, kann er einen Fehler zurück, wie diese Eigenschaft, um festgelegt wird **"true"**. Wenn kein Fehler zurückgegeben wird, ignoriert er die Anforderung zum Vorbereiten der Befehl und legt die **Prepared** Eigenschaft **"false"**.

