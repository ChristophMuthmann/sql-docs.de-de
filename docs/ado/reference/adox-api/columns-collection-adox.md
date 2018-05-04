---
title: Columns-Auflistung (ADOX) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f3210bf977a27e945f2faa8e80e8a7c72cbe5cf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="columns-collection-adox"></a>Columns-Auflistung (ADOX)
Enthält alle [Spalte](../../../ado/reference/adox-api/column-object-adox.md) Objekte von einer Tabelle, Index oder Schlüssel.  
  
## <a name="remarks"></a>Hinweise  
 Die [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) Methode für eine **Spalten** Auflistung für ADOX eindeutig ist. Folgende Aktionen sind möglich:  
  
-   Fügen Sie eine neue Spalte in der Auflistung der **Append** Methode.  
  
 Die übrigen Eigenschaften und Methoden sind standard in ADO-Auflistungen. Folgende Aktionen sind möglich:  
  
-   Zugriff auf eine Spalte in der Auflistung mit den [Element](../../../ado/reference/ado-api/item-property-ado.md) Eigenschaft.  
  
-   Zurückgeben der Anzahl der Spalten in der Auflistung mit den [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft.  
  
-   Entfernen einer Spalte aus der Auflistung mit den [löschen](../../../ado/reference/adox-api/delete-method-adox-collections.md) Methode.  
  
-   Aktualisieren Sie die Objekte in der Auflistung entsprechend der aktuellen Datenbank-Schema mit dem [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode.  
  
> [!NOTE]
>  Beim Anfügen, wird ein Fehler auftreten eine **Spalte** auf die **Spalten** Auflistung von ein [Index](../../../ado/reference/adox-api/index-object-adox.md) Wenn der **Spalte** ist nicht in einem [Tabelle](../../../ado/reference/adox-api/table-object-adox.md) , ist bereits angefügt, um die [Tabellen](../../../ado/reference/adox-api/tables-collection-adox.md) Auflistung.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Columns Collection Properties, Methods, and Events (Columns-Auflistung – Eigenschaften, Methoden und Ereignisse)](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Append-Methode, Beispiel für Name-Eigenschaft (VB) Spalten und Tabellen](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection-Methode schließen, Beispiel für die Tabelle Type-Eigenschaft (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Beispiel für ParentCatalog-Eigenschaft (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder-Eigenschaft (VB)-Beispiel](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column-Objekt (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
