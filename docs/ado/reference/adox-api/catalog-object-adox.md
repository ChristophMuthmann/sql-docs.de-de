---
title: Catalog-Objekt (ADOX) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d8f47b63022f481c5ed102bcc9e97f5fa563aea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="catalog-object-adox"></a>Katalogobjekt (ADOX)
Enthält Auflistungen ([Tabellen](../../../ado/reference/adox-api/tables-collection-adox.md), [Ansichten](../../../ado/reference/adox-api/views-collection-adox.md), [Benutzer](../../../ado/reference/adox-api/users-collection-adox.md), [Gruppen](../../../ado/reference/adox-api/groups-collection-adox.md), und [Prozeduren](../../../ado/reference/adox-api/procedures-collection-adox.md)), Beschreiben Sie den Katalog Schema mit einer Datenquelle.  
  
## <a name="remarks"></a>Hinweise  
 Sie können die **Katalog** Objekt durch Hinzufügen oder Entfernen von Objekten oder durch Ändern von vorhandenen Objekten. Einige Anbieter unterstützen möglicherweise nicht alle von der **Katalog** Objekte oder unterstützen nur das Anzeigen von Schemainformationen.  
  
 Mit den Eigenschaften und Methoden von einem **Katalog** -Objekt können Sie:  
  
-   Öffnen des Katalogs durch Festlegen der [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) Eigenschaft, um eine ADO [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt oder eine gültige Verbindungszeichenfolge.  
  
-   Erstellen Sie einen neuen Katalog mit den [erstellen](../../../ado/reference/adox-api/create-method-adox.md) Methode.  
  
-   Bestimmen der Besitzer der Objekte in einem **Katalog** mit der [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) und [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) Methoden.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Error-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Katalog ActiveConnection-Eigenschaft (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Befehl "und" CommandText-Eigenschaft-Beispiel (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Connection-Methode schließen, Beispiel für die Tabelle Type-Eigenschaft (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create-Methode-Beispiel (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters-Auflistung, Eigenschaft Befehlsbeispiel (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Beispiel für ParentCatalog-Eigenschaft (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Prozeduren Append-Methode (Beispiel) (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Prozeduren löschen Methodenbeispiel (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Prozeduren aktualisiert Methodenbeispiel (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Ansichten und Felder Beispiel für Auflistungen (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Ansichten Append-Methode (Beispiel) (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views-Auflistung, CommandText-Eigenschaft (VB)-Beispiel](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Ansichten löschen Methodenbeispiel (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Ansichten aktualisieren Methodenbeispiel (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Groups-Auflistung (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Prozeduren-Auflistung (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Tables-Auflistung (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Views-Auflistung (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
