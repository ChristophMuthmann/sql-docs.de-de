---
title: Übergeben von Parametern an einen benannten Befehl | Microsoft Docs
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
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db51630bf9629920ce91af22fc731f3a5c919fd0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="passing-parameters-to-a-named-command"></a>Übergeben von Parametern an einen benannten Befehl
So fest, wie das Ergebnis des Befehls als, out übergeben wird ein *out* Variablen von der genannte Befehl, Parameter wurde für ein parametrisierter Befehl kann als übergebene *in* Variablen in der genannte Befehl.  
  
 Im folgenden Codebeispiel wird versucht, alle Aufträge Abrufen vom Kunden aufgegebene, deren **CustomerID** "ALKFI" aus der Northwind-Datenbank ist. Der Wert der **CustomerID** angegeben wird, zu dem Zeitpunkt, wenn der genannte Befehl aufgerufen wird.  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 Beachten Sie, dass alle Eingabeparameter müssen eine Output-Variable vor und die Datentypen der Parameter übereinstimmen, oder konvertiert werden können, mit denen die entsprechenden Felder ein. Die folgende Anweisung:  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 – führt zu einem Fehler nicht übereinstimmende Datentypen, weil der erforderliche Eingabeparameter ist eine **Zeichenfolge** Typ nicht von einer **ganze Zahl** Typ.  
  
 Der folgende Aufruf:  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 – ist gültig, aber ergibt ein leeres Resultset, weil keine solche Einträge in der Datenbank vorhanden sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
