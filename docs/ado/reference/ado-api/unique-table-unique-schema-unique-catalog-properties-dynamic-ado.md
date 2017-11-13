---
title: "Steuerelement ändert sich in Basistabelle von Recordsets (ADO) | Microsoft Docs"
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
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da2f70b0f3d6f1ae3983e44f26191e13cc26f5a2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Eindeutige Tabelle, eindeutiges Schema, eindeutige Catalog (ADO) für das dynamische Eigenschaften
Ermöglicht es Ihnen zu eng Steuerelement Änderungen an einer bestimmten Basistabelle in eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , die durch eine Joinoperation für mehrere Basistabellen gebildet wurde.  
  
-   **Eindeutige Tabelle** gibt den Namen der Basistabelle, auf denen Updates, einfügungen und löschungen zulässig sind.  
  
-   **Eindeutiges Schema** gibt an, die *Schema*, oder der Name des Besitzers der Tabelle.  
  
-   **Eindeutige Katalog** gibt an, die *Katalog*, oder der Name der Datenbank, die die Tabelle enthält.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert, der den Namen der Tabellen, Schema oder Katalog ist.  
  
## <a name="remarks"></a>Hinweise  
 Die gewünschte Basistabelle wird durch seine Katalog, Schema und Tabellennamen eindeutig identifiziert. Wenn die **eindeutige Tabelle** Eigenschaft festgelegt ist, werden die Werte der der **eindeutiges Schema** oder **Unique Catalog** Eigenschaften werden verwendet, um die Basistabelle zu suchen. Ist vorgesehen, aber nicht erforderlich, eine oder beide der **eindeutiges Schema** und **Unique Catalog** Eigenschaften festgelegt werden, bevor die **eindeutige Tabelle** festgelegt wird.  
  
 Der Primärschlüssel der der **eindeutige Tabelle** so behandelt, als den primären Schlüssel für die gesamte **Recordset**. Dies ist der Schlüssel, der für jede Methode erfordert einen Primärschlüssel verwendet wird.  
  
 Während **eindeutige Tabelle** festgelegt ist, die [löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md) Methode betrifft nur die benannte Tabelle. Die [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [Update](../../../ado/reference/ado-api/update-method.md), und [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methoden Auswirkungen auf alle entsprechenden zugrunde liegenden Basistabellen der **Recordset**.  
  
 **Eindeutige Tabelle** muss vor dem Ausführen alle benutzerdefinierten neusynchronisierungen angegeben werden. Wenn **eindeutige Tabelle** wurde nicht angegeben, die [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) Eigenschaft hat keine Auswirkung.  
  
 Ein Laufzeitfehler ausgegeben, wenn eine eindeutige Basistabelle nicht gefunden werden kann.  
  
 Diese dynamischen Eigenschaften werden an angehängt der **Recordset** Objekt [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung bei der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) -Eigenschaftensatz auf  **AdUseClient**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

