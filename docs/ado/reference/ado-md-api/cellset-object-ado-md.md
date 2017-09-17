---
title: Cellset-Objekt (ADO MD) | Microsoft Docs
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
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f53e9ec68a4375a9c8d07dc3937750c2e7ba3d46
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="cellset-object-ado-md"></a>Cellset-Objekt (ADO MD)
Stellt die Ergebnisse einer MDX-Abfrage. Es ist eine Ansammlung von Zellen, die aus Cubes oder anderen Cellsets ausgewählt wurden.  
  
## <a name="remarks"></a>Hinweise  
 Daten in einem **Cellset** werden mithilfe von direkten, arrayähnlichen Zugriff abgerufen. Sie können einen Drilldown zum einen bestimmten Member zum Abrufen von Daten über diesen Member ausführen. Z. B. der folgende Code gibt die Beschriftung des ersten Elements in der ersten Position auf der ersten Achse eines cellSets mit dem Namen `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Hinweise  
 Es gibt keine aktuelle Zelle innerhalb eines cellSets dar. Stattdessen die [Element](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) Eigenschaft ruft eine bestimmte [Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md) Objekt aus dem Cellset. Die Argumente der **Element** Eigenschaft zu bestimmen, welche Zelle abgerufen wird. Sie können den eindeutigen Ordnungswert einer Zelle angeben. Sie können Zellen auch abrufen, mit deren Positionsnummern an jeder Achse der das Cellset. Weitere Informationen zum Abrufen von Zellen finden Sie unter der [Element](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) Eigenschaft.  
  
 Mit den Auflistungen, Methoden und Eigenschaften von einer **Cellset** -Objekts können Sie folgende Möglichkeiten:  
  
-   Ordnen Sie eine offene Verbindung mit einer **Cellset** Objekt durch Festlegen seiner [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) Eigenschaft.  
  
-   Ausführen und zum Abrufen der Ergebnisse einer MDX-Abfrage mit der [öffnen](../../../ado/reference/ado-md-api/open-method-ado-md.md) Methode.  
  
-   Abrufen einer **Zelle** aus der **Cellset** mit der [Element](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) Eigenschaft.  
  
-   Zurückgeben der [Achse](../../../ado/reference/ado-md-api/axis-object-ado-md.md) Objekten, definieren die **Cellset** mit der [Achsen](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) Auflistung.  
  
-   Abrufen von Informationen zu den Dimensionen zum Filtern der Daten in der **Cellset** mit der [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben, oder geben Sie die Abfrage, die zum Definieren der **Cellset** mit der [Quelle](../../../ado/reference/ado-md-api/source-property-ado-md.md) Eigenschaft.  
  
-   Zurückgeben des aktuellen Status von der **Cellset** (geöffnet, geschlossen, ausgeführt wird, oder eine Verbindung herstellen) mit der [Zustand](../../../ado/reference/ado-md-api/state-property-ado-md.md) Eigenschaft.  
  
-   Schließen Sie ein offenes **Cellset** mit der [schließen](../../../ado/reference/ado-md-api/close-method-ado-md.md) Methode.  
  
-   Anbieterspezifische Informationen zum Abrufen der **Cellset** mit dem standard ADO [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Cellset-Beispiel (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Die Achsenauflistung (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Cell-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
