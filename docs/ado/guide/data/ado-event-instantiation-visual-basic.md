---
title: 'ADO-Ereignis-Instanziierung: Visual Basic | Microsoft Docs'
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
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bfcca102fc9e52070ceb5c982972537ecc6e571d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO-Ereignis-Instanziierung: Visual Basic
Damit ADO-Ereignisse in Microsoft® Visual Basic® behandeln zu können, müssen Sie deklarieren, einer auf Modulebene Variable mit dem **WithEvents** Schlüsselwort. Die Variable kann nur als Teil eines Moduls Klasse deklariert werden und muss auf der Modulebene deklariert werden. Dies ist nicht so restriktiv wie es, aber scheint da Visual Basic **Formular** Objekte sind auch Klassen. Die einfachste Möglichkeit, ADO-Ereignisse behandeln wird zum Deklarieren einer Variablen mit **WithEvents**. Das folgende Beispiel verarbeitet die **ConnectComplete** -Ereignis für ein **Verbindung** Objekt:  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 Die **Verbindung** Deklaration Objekts, auf die **Formular** Ebene mithilfe der **WithEvents** Schlüsselwort, um die Behandlung von Ereignissen zu aktivieren. Der Ereignishandler Form_Load erstellt das Objekt tatsächlich durch Zuweisung eines neuen **Verbindung** -Objekt *ConnEvent* und öffnet dann die Verbindung. Natürlich dazu eine realen Anwendung weitere Verarbeitung im Ereignishandler Form_Load als hier angezeigt wird.
