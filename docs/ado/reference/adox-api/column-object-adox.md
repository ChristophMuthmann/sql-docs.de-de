---
title: Column-Objekt (ADOX) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5a8a5047f4cd4655ebe1dd041e44949ca361c54
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="column-object-adox"></a>Column-Objekt (ADOX)
Stellt eine Spalte aus einer Tabelle, Index oder Schlüssel.  
  
## <a name="remarks"></a>Hinweise  
 Der folgende Code erstellt ein neues **Spalte**:  
  
 `Dim obj As New Column`  
  
 Mit den Eigenschaften und Auflistungen von einer **Spalte** -Objekt können Sie:  
  
-   Identifizieren Sie die Spalte mit dem [Name-Eigenschaft (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft.  
  
-   Geben Sie die Spalte mit den Daten der [Typeigenschaft (Schlüssel) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) Eigenschaft.  
  
-   Bestimmen, ob die Spalte fester Länge ist oder wenn es mit null-Werte enthalten kann die [Attribute-Eigenschaft (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) Eigenschaft.  
  
-   Geben Sie die maximale Größe der Spalte mit dem [DefinedSize-Eigenschaft (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) Eigenschaft.  
  
-   Geben Sie für numerische Werte, mit dem [NumericScale-Eigenschaft (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) Eigenschaft.  
  
-   Geben Sie die maximale Genauigkeit mit numerischen Datenwert der [Precision-Eigenschaft (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) Eigenschaft.  
  
-   Geben Sie die [Katalog-Objekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) , besitzt die Spalte mit dem [ParentCatalog-Eigenschaft (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) Eigenschaft.  
  
-   Für Schlüsselspalten, geben Sie den Namen der verknüpften Spalte in der verknüpften Tabelle mit den [RelatedColumn-Eigenschaft (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) Eigenschaft.  
  
-   Für Indexspalten angeben, ob die Sortierreihenfolge aufsteigend oder absteigend mit ist der [SortOrder-Eigenschaft (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) Eigenschaft.  
  
-   Zugriff auf die anbieterspezifischen Eigenschaften mit den [Eigenschaften-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
> [!NOTE]
>  Nicht alle Eigenschaften der **Spalte** Objekte können von Ihren Datenanbieter unterstützt werden. Es wird eine Fehlermeldung angezeigt, wenn Sie einen Wert für eine Eigenschaft festgelegt haben, die vom Anbieter nicht unterstützt werden. Für das neue **Spalte** Objekte aufweist, tritt der Fehler auf, wenn das Objekt der Auflistung hinzugefügt wird. Für vorhandene Objekte tritt der Fehler beim Festlegen der Eigenschaft.  
>   
>  Beim Erstellen **Spalte** -Objekten, das Vorhandensein des ein geeigneter Standardwert für eine optionale Eigenschaft kann nicht garantiert, dass Ihr Anbieter die Eigenschaft unterstützt. Weitere Informationen über die Eigenschaften, die Ihr Anbieter unterstützt, finden Sie in der Dokumentation Ihres Anbieters.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Spalte-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Append-Methode, Beispiel für Name-Eigenschaft (VB) Spalten und Tabellen](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection-Methode schließen, Beispiel für die Tabelle Type-Eigenschaft (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX-Codebeispiel: NumericScale und Genauigkeit Eigenschaften-Beispiel (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Beispiel für ParentCatalog-Eigenschaft (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder-Eigenschaft (VB)-Beispiel](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns-Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
