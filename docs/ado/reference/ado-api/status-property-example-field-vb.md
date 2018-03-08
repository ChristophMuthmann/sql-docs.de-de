---
title: Beispiel der Status-Eigenschaft (Feld) (VB) | Microsoft Docs
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
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ea3ebba271ebdc12802b31cc1f50cdd3befead0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="status-property-example-field-vb"></a>Beispiel der Status-Eigenschaft (Feld) (VB)
Das folgende Beispiel öffnet ein Dokument aus einen Ordner mit Lese-/Schreibzugriff der [Publishing Internetanbieter](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Die [Status](../../../ado/reference/ado-api/status-property-ado-field.md) Eigenschaft eine [Feld](../../../ado/reference/ado-api/field-object.md) Objekt des der [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) zuerst festgelegt, um **AdFieldPendingInsert**, und klicken Sie dann auf den aktualisiertwerden**AdFieldOk**.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=http://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 Das folgende Beispiel löscht einen bekannten **Feld** aus einem **Datensatz** aus einem Dokument geöffnet. Die **Status** wird zuerst-Eigenschaftensatz auf **AdFieldOK**, klicken Sie dann **AdFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 Der folgende code Löscht ein **Feld** aus einem **Datensatz** für ein Dokument schreibgeschützt geöffnet. **Status** festgelegt, um **AdFieldPendingDelete**. Am [Update](../../../ado/reference/ado-api/update-method.md), schlägt der Löschvorgang fehl und **Status** werden **AdFieldPendingDelete** plus **AdFieldPermissionDenied**. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) löscht die ausstehende **Status** Einstellung.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)   
 [Record Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status-Eigenschaft (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
