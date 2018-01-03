---
title: Aufrufen einer gespeicherten Prozedur mit einem Befehl | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e6c22f098efcb2352e450c07aece8f88c8f32b4d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Aufrufen einer gespeicherten Prozedur mit einem Befehl
Sie können einen Befehl verwenden, um eine gespeicherte Prozedur aufzurufen. Im Codebeispiel am Ende dieses Themas bezieht sich auf eine gespeicherte Prozedur in der Northwind-Beispieldatenbank namens CustOrdersOrders, die wie folgt definiert ist.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 SQL Server-Dokumentation für Weitere Informationen zum Definieren und Aufrufen von gespeicherten Replikationsprozeduren angezeigt.  
  
 Diese gespeicherte Prozedur ähnelt den Befehl ab, die [Objekt Befehlsparameter](../../../ado/guide/data/command-object-parameters.md). Es dauert eine Kunden-ID-Parameter und gibt Informationen zu den Bestellungen dieses Kunden zurück. Im folgenden Codebeispiel verwendet diese gespeicherte Prozedur als Quelle für ein ADO **Recordset**.  
  
 Mithilfe der gespeicherten Prozedur können Sie eine weitere Funktion von ADO zuzugreifen: die **Parameter** Auflistung **aktualisieren** Methode. Mithilfe dieser Methode kann ADO automatisch alle Informationen zu den Parametern, die den Befehl zur Laufzeit erforderlichen ausfüllen. Durch diese Technik wird zu Leistungseinbußen, da die Datenquelle für die Informationen zu den Parametern ADO Abfrage ausführen muss.  
  
 Andere wichtige Unterschiede zwischen den im folgenden Codebeispiel wird und der Code in [Objekt Befehlsparameter](../../../ado/guide/data/command-object-parameters.md), wobei die Parameter manuell eingegeben wurden. Zunächst diesen Code nicht festgelegt die **Prepared** Eigenschaft **"true"** da dies eine gespeicherte SQL Server-Prozedur ist und ist per Definition vorkompiliert. Zweitens die **Befehlstyp (CommandType)** Eigenschaft von der **Befehl** Objekt geändert wird, um **AdCmdStoredProc** im zweiten Beispiel ADO informiert, dass der Befehl eine gespeicherte Prozedur wurde.  
  
 Schließlich muss im zweiten Beispiel die Parameter durch Index verwiesen werden beim Festlegen des Werts, da Sie möglicherweise nicht den Namen des Parameters zur Entwurfszeit bekannt. Wenn Sie den Namen des Parameters kennen, legen Sie die neue [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) Eigenschaft von der **Befehl** Objekt auf "true", und finden Sie in der Name der Eigenschaft. Sie Fragen sich vielleicht, warum die Position des ersten Parameters in der gespeicherten Prozedur erwähnt (@CustomerID) 1 statt 0 (`objCmd(1) = "ALFKI"`). Dies ist da Parameter 0 Rückgabewert für die gespeicherte SQL Server-Prozedur enthält.  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
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
'EndAutoParamCmd  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Knowledge Base-Artikel 117500](http://go.microsoft.com/fwlink/?LinkId=117500)
