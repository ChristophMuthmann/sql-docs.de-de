---
title: Katalog ActiveConnection (VB-Beispiel) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc353766a68dc32a96842a9102434511740f34c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-activeconnection-property-example-vb"></a>Beispiel für Katalog ActiveConnection-Eigenschaft (VB)
Festlegen der [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) Eigenschaft, um eine gültige, offene Verbindung "geöffnet" des Katalogs. Aus einem Katalog öffnen können Sie die Schemaobjekte in diesem Katalog zugreifen.  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 Festlegen der **ActiveConnection** Eigenschaft, um eine gültige Verbindungszeichenfolge auch "öffnet" des Katalogs.  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveConnection-Eigenschaft (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table-Objekt (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Tables-Auflistung (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type-Eigenschaft (Tabelle) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
