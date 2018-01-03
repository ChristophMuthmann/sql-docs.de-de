---
title: NumericScale und Genauigkeit Eigenschaften-Beispiel (VB) | Microsoft Docs
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
- Precision property [ADOX], Visual Basic example
- NumericScale property [ADOX], Visual Basic example
ms.assetid: ea2ec614-34c8-41b7-8ebd-063798bd56b4
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37957a75306abb18de656aa6418f3bc08b8c4ab6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="adox-code-example-numericscale-and-precision-properties-example-vb"></a>ADOX-Codebeispiel: NumericScale und Genauigkeit Eigenschaften-Beispiel (VB)
In diesem Beispiel wird veranschaulicht, die [NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md) und [Genauigkeit](../../../ado/reference/adox-api/precision-property-adox.md) Eigenschaften der [Spalte](../../../ado/reference/adox-api/column-object-adox.md) Objekt. Dieser Code zeigt an, deren Wert für die **Bestelldetails** Tabelle mit den *Northwind* Datenbank.  
  
```  
' BeginNumericScalePrecVB  
Sub Main()  
    On Error GoTo NumericScalePrecXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblOD As ADOX.Table  
    Dim colLoop As ADOX.Column  
  
    ' Connect the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "data source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve the Order Details table  
    Set tblOD = cat.Tables("Order Details")  
  
    ' Display numeric scale and precision of  
    ' small integer fields.  
    For Each colLoop In tblOD.Columns  
        If colLoop.Type = adSmallInt Then  
            MsgBox "Column: " & colLoop.Name & vbCr & _  
                "Numeric scale: " & _  
                colLoop.NumericScale & vbCr & _  
                "Precision: " & colLoop.Precision  
        End If  
    Next colLoop  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
NumericScalePrecXError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndNumericScalePrecVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Column-Objekt (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [NumericScale-Eigenschaft (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)   
 [Precision-Eigenschaft (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)
