---
title: Mithilfe eines Recordset-Objekts | Microsoft Docs
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
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2377c2bf7d6825c8395893b35350b48dab53167e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-a-recordset-object"></a>Mithilfe eines Recordset-Objekts
Alternativ können Sie **Recordset.Open** implizit eine Verbindung herzustellen und Ausgeben eines Befehls über diese Verbindung in einem einzigen Vorgang. Beispielsweise ist in Visual Basic:  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 Beachten Sie, dass **oRs.Open** nimmt eine Verbindungszeichenfolge (*sConn*), anstelle von einer **Verbindung** Objekt (*oConn*), als Wert für die  **ActiveConnection** Parameter. Auch die clientseitigen Cursortyp erzwungen wird, durch Festlegen der **CursorLocation** Eigenschaft auf die **Recordset** Objekt. Vergleichen Sie dies mit erneut, den **HelloData** Beispiel.
