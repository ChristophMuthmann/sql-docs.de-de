---
title: Tables-Auflistung (ADOX) | Microsoft Docs
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
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80093f384c8b25f16b59b267429675566ff94ddf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tables-collection-adox"></a>Tables-Auflistung (ADOX)
Enthält alle [Tabelle](../../../ado/reference/adox-api/table-object-adox.md) Objekte eines Katalogs.  
  
## <a name="remarks"></a>Hinweise  
 Die [Append](../../../ado/reference/adox-api/append-method-adox-tables.md) Methode für eine **Tabellen** Auflistung für ADOX eindeutig ist. Folgende Aktionen sind möglich:  
  
-   Hinzufügen einer neuen Tabelle in der Auflistung der **Append** Methode.  
  
 Die übrigen Eigenschaften und Methoden sind standard in ADO-Auflistungen. Folgende Aktionen sind möglich:  
  
-   Zugreifen auf eine Tabelle in der Auflistung mit den [Element](../../../ado/reference/ado-api/item-property-ado.md) Eigenschaft.  
  
-   Zurückgeben der Anzahl der Tabellen in der Auflistung mit den [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft.  
  
-   Entfernen einer Tabelle aus der Auflistung mit den [löschen](../../../ado/reference/adox-api/delete-method-adox-collections.md) Methode.  
  
-   Aktualisieren Sie die Objekte in der Auflistung entsprechend das Schema der aktuellen Datenbank mit der [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode.  
  
 Einige Anbieter möglicherweise andere Schemaobjekte, z. B. eine Sicht zurück, der **Tabellen** Auflistung. Deshalb können einige Auflistungen ADOX mehrere Verweise auf dasselbe Objekt enthalten. Sollten Sie das Objekt löschen aus einer Auflistung, die Änderung werden nicht sichtbar, in einer anderen Sammlung, die das gelöschte Objekt bis verweist auf die **aktualisieren** Methode wird aufgerufen, in der Auflistung. Z. B. mit dem OLE DB-Anbieter für Microsoft Jet Ansichten werden zurückgegeben, mit der **Tabellen** Auflistung. Wenn Sie eine Sicht löschen, müssen Sie aktualisieren die **Tabellen** Auflistung, bevor die Sammlung wird die Änderung zu übernehmen.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Tables Collection Properties, Methods, and Events (Tables-Auflistung – Eigenschaften, Methoden und Ereignisse)](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Katalog ActiveConnection-Eigenschaft (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Append-Methode, Beispiel für Name-Eigenschaft (VB) Spalten und Tabellen](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection-Methode schließen, Beispiel für die Tabelle Type-Eigenschaft (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table-Objekt (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
