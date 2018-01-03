---
title: "Speichern und öffnen Sie die Methoden-Beispiel (VB) | Microsoft Docs"
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
dev_langs: VB
helpviewer_keywords:
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26fa69e0c02dfffb208725f61c826068337a8b98
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="save-and-open-methods-example-vb"></a>Speichern Sie und öffnen Sie die Methoden-Beispiel (VB)
Diese drei Beispielen wird gezeigt, wie die [speichern](../../../ado/reference/ado-api/save-method.md) und [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methoden können zusammen verwendet werden.  
  
 Angenommen Sie, Sie werden auf einer Geschäftsreise und eine Tabelle aus einer Datenbank mitnehmen möchten. Bevor Sie fortfahren, Sie greifen auf die Daten als ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) und speichern Sie sie in einem Formular übertragbar. Wenn Sie sich an Ihr Ziel ankommen, Zugriff auf die **Recordset** als ein lokaler getrennt **Recordset**. Nehmen Sie Änderungen an der **Recordset**, und speichern Sie es erneut. Schließlich bei der Rückgabe home, Sie erneut mit der Datenbank verbunden und mit unterwegs vorgenommenen Änderungen zu aktualisieren.  
  
 Erstens zugreifen, und speichern Sie die ***Autoren*** Tabelle.  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 An diesem Punkt haben Sie an Ihrem Ziel angekommen ist. Greifen Sie auf die ***Autoren*** Tabelle als eine lokale getrennt **Recordset**. Sie benötigen die **MSPersist** Anbieter auf dem Computer, die Sie verwenden, um den Zugriff auf die gespeicherte Datei a:\Pubs.xml.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Schließlich zurückgestellt Startseite. Jetzt können aktualisieren Sie die Datenbank mit Änderungen.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Weitere Informationen zum Recordset Persistenz](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)
