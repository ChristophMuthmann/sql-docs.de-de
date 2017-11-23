---
title: "Ansichten löschen Methodenbeispiel (VB) | Microsoft Docs"
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
helpviewer_keywords: Delete method [ADOX]
ms.assetid: 17df2a83-4166-4df8-8c17-0a33aaac8582
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68a731495fdbf6a71d121b84f322e1d5df68342f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="views-delete-method-example-vb"></a>Ansichten löschen Methodenbeispiel (VB)
Der folgende Code zeigt, wie Sie die [löschen](../../../ado/reference/adox-api/delete-method-adox-collections.md) Methode, um eine Sicht aus dem Katalog gelöscht.  
  
```  
' BeginDeleteViewVB  
Sub Main()  
    On Error GoTo DeleteViewError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    'Delete the View  
    cat.Views.Delete "AllCustomers"  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteViewError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteViewVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Delete-Methode (ADOX Sammlungen)](../../../ado/reference/adox-api/delete-method-adox-collections.md)   
 [Views-Auflistung (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
