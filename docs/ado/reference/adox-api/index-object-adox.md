---
title: Index-Objekt (ADOX) | Microsoft Docs
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
apitype: COM
f1_keywords: Index
helpviewer_keywords: Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 584ab3c0bb5bb4616df21598d36da1b6e729d9fa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="index-object-adox"></a>Index-Objekt (ADOX)
Stellt einen Index aus einer Datenbanktabelle dar.  
  
## <a name="remarks"></a>Hinweise  
 Der folgende Code erstellt ein neues **Index**:  
  
```  
Dim obj As New Index  
```  
  
 Mit den Eigenschaften und Auflistungen von einer **Index** -Objekt können Sie:  
  
-   Identifizieren Sie den Index mit der [Namen](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft.  
  
-   Zugreifen auf die Datenbankspalten des Indexes mit der [Spalten](../../../ado/reference/adox-api/columns-collection-adox.md) Auflistung.  
  
-   Gibt an, ob die Indexschlüssel eindeutig sein müssen die [Unique](../../../ado/reference/adox-api/unique-property-adox.md) Eigenschaft.  
  
-   Gibt an, ob der Index der Primärschlüssel für eine Tabelle mit ist der [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) Eigenschaft.  
  
-   Gibt an, ob Datensätze mit null-Werte in ihren Indexfelder Indexeinträge verfügen die [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) Eigenschaft.  
  
-   Gibt an, ob der Index gruppiert ist, mit der [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) Eigenschaft.  
  
-   Zugriff auf die anbieterspezifischen Eigenschaften mit den [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
> [!NOTE]
>  Beim Anfügen, wird ein Fehler auftreten eine [Spalte](../../../ado/reference/adox-api/column-object-adox.md) auf die **Spalten** Auflistung von ein **Index** Wenn der **Spalte** ist nicht in einem [Tabelle](../../../ado/reference/adox-api/table-object-adox.md) -Objekt bereits angefügt, um die [Tabellen](../../../ado/reference/adox-api/tables-collection-adox.md) Auflistung.  
  
> [!NOTE]
>  Der Datenanbieter unterstützen möglicherweise nicht alle Eigenschaften des **Index** Objekte. Wenn Sie einen Wert für eine Eigenschaft festgelegt haben, die vom Anbieter nicht unterstützt wird, wird eine Fehlermeldung angezeigt. Für das neue **Index** Objekte aufweist, tritt der Fehler auf, wenn das Objekt der Auflistung hinzugefügt wird. Für vorhandene Objekte tritt der Fehler beim Festlegen der Eigenschaft.  
  
> [!NOTE]
>  Beim Erstellen **Index** -Objekten, das Vorhandensein des ein geeigneter Standardwert für eine optionale Eigenschaft kann nicht garantiert, dass Ihr Anbieter die Eigenschaft unterstützt. Weitere Informationen über die Eigenschaften, die Ihr Anbieter unterstützt, finden Sie in der Dokumentation Ihres Anbieters.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Index-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Indizes Append-Methode (Beispiel) (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Beispiel für IndexNulls-Eigenschaft (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey und eindeutige Eigenschaften-Beispiel (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder-Eigenschaft (VB)-Beispiel](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns-Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Auflistung von Indizes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
