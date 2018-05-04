---
title: Table-Objekt (ADOX) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 904521c4a306fc5cf0ecf3f2dced169404f70f14
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="table-object-adox"></a>Table-Objekt (ADOX)
Stellt eine Datenbanktabelle, einschließlich Spalten, Indizes und Schlüssel dar.  
  
## <a name="remarks"></a>Hinweise  
 Der folgende Code erstellt ein neues **Tabelle**:  
  
```  
Dim obj As New Table  
```  
  
 Mit den Eigenschaften und Auflistungen von einer **Tabelle** -Objekt können Sie:  
  
-   Identifizieren Sie die Tabelle mit den [Name-Eigenschaft (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft.  
  
-   Bestimmen Sie die Art der Tabelle mit den [Typeigenschaft (Tabelle) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) Eigenschaft.  
  
-   Zugriff auf die Datenbankspalten der Tabelle mit den [Spalten Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) Auflistung.  
  
-   Zugreifen auf die Indizes der Tabelle mit den [Indizes-Auflistung (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Zugreifen auf die Schlüssel der Tabelle mit den [Schlüssel Auflistung (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Geben Sie den Katalog, der die Tabelle besitzt die [ParentCatalog-Eigenschaft (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) Eigenschaft.  
  
-   Rückgabeinformationen Datum mit dem [DateCreated-Eigenschaft (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) und [DateModified-Eigenschaft (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) Eigenschaften.  
  
-   Zugriff auf die anbieterspezifischen Eigenschaften mit den [Eigenschaften-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
> [!NOTE]
>  Der Datenanbieter unterstützen möglicherweise nicht alle Eigenschaften des **Tabelle** Objekte. Es wird eine Fehlermeldung angezeigt, wenn Sie einen Wert für eine Eigenschaft festgelegt haben, die vom Anbieter nicht unterstützt werden. Für das neue **Tabelle** Objekte aufweist, tritt der Fehler auf, wenn das Objekt der Auflistung hinzugefügt wird. Für vorhandene Objekte tritt der Fehler beim Festlegen der Eigenschaft.  
>   
>  Beim Erstellen **Tabelle** -Objekten, das Vorhandensein des ein geeigneter Standardwert für eine optionale Eigenschaft kann nicht garantiert, dass Ihr Anbieter die Eigenschaft unterstützt. Weitere Informationen über die Eigenschaften, die Ihr Anbieter unterstützt, finden Sie in der Dokumentation Ihres Anbieters.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Table-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Katalog ActiveConnection-Eigenschaft (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Append-Methode, Beispiel für Name-Eigenschaft (VB) Spalten und Tabellen](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection-Methode schließen, Beispiel für die Tabelle Type-Eigenschaft (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Beispiel für ParentCatalog-Eigenschaft (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Columns-Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Auflistung von Indizes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Die Auflistung der Schlüssel (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables-Auflistung (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
