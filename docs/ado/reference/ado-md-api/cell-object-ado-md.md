---
title: Cell-Objekt (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6ef6e4e3cf888b60050bfd297863568d8112a57
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="cell-object-ado-md"></a>Cell-Objekt (ADO MD)
Stellt die Daten am Schnittpunkt der Achsenkoordinaten enthaltenen im Cellset dar.  
  
## <a name="remarks"></a>Hinweise  
 Ein **Zelle** -Objekt zurück, die [Element](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) Eigenschaft eine [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) Objekt.  
  
 Die Auflistungen und Eigenschaften einer **Zelle** -Objekts können Sie folgende Möglichkeiten:  
  
-   Zurückgeben der Daten in der **Zelle** mit der [Wert](../../../ado/reference/ado-md-api/value-property-ado-md.md) Eigenschaft.  
  
-   Die Zeichenfolge zurückgegeben, die die formatierte Anzeige der darstellt der **Wert** Eigenschaft mit dem [FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) Eigenschaft.  
  
-   Den Ordinalwert des Zurückgeben der **Zelle** innerhalb der **Cellset** mit der [Ordinal](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) Eigenschaft.  
  
-   Bestimmen Sie die Position des der **Zelle** innerhalb der [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) mit der [Positionen](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) Auflistung.  
  
-   Weitere Informationen zum Abrufen der **Zelle** mit dem standard ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
 Die **Eigenschaften** Auflistung enthält Eigenschaften, die vom Anbieter bereitgestellt. Die folgende Tabelle enthält Eigenschaften, die möglicherweise zur Verfügung. Die tatsächliche Eigenschaftenliste kann je nach der Implementierung des Anbieters abweichen. Siehe die Dokumentation für Ihren Anbieter für eine vollständige Liste der verfügbaren Eigenschaften.  
  
|Name|Description|  
|----------|-----------------|  
|Hintergrundfarbe|Background-Farbe ab die Zelle angezeigt wird.|  
|FontFlags|Bitmaske, die Auswirkungen auf die Schriftart detailliert angibt.|  
|FontName|Der Wert der Zelle anzuzeigenden verwendete Schriftart.|  
|FontSize|Der Wert der Zelle anzuzeigenden verwendeten Schriftgrad.|  
|Vordergrundfarbe|Die Vordergrundfarbe ab die Zelle angezeigt wird.|  
|FormatString|Der Wert in eine formatierte Zeichenfolge.|  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Achse-Beispiel (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Positionen-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

