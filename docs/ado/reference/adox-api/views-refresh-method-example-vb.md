---
title: Ansichten aktualisieren Methodenbeispiel (VB) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6e526091804e36790f79a051399ff69e479df4a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="views-refresh-method-example-vb"></a>Ansichten aktualisieren Methodenbeispiel (VB)
Der folgende Code zeigt die Vorgehensweise beim Aktualisieren der [Ansichten](../../../ado/reference/adox-api/views-collection-adox.md) Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md). Dies ist erforderlich, bevor Sie [Ansicht](../../../ado/reference/adox-api/view-object-adox.md) Objekte aus der **Katalog** zugegriffen werden kann.  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Refresh-Methode (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Views-Auflistung (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)

