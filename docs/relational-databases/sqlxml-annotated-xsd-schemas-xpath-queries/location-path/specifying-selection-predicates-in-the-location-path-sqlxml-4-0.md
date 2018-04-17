---
title: Angeben von Auswahlprädikaten im Speicherortpfad (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 67cbd749cf3293b6a20b55581648ff6cbfa6ddf5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>Angeben von Auswahlprädikaten im Speicherortpfad (SQLXML 4.0) 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ein Prädikat filtert eine Knotengruppe in Bezug auf eine Achse (ähnlich einer WHERE-Klausel in einer SELECT-Anweisung). Das Prädikat wird zwischen Klammern angegeben. Für jeden Knoten in der zu filternden Knotengruppe wird der Prädikatausdruck mit dem entsprechenden Knoten als Kontextknoten ausgewertet. Die Anzahl der Knoten in der Knotengruppe dient dabei als Kontextgröße. Ergibt die Auswertung des Prädikatausdrucks für den betreffenden Knoten TRUE, wird dieser Knoten in die resultierende Knotengruppe aufgenommen.  
  
 XPath ermöglicht auch die positionsbasierte Filterung. Ein Prädikatausdruck, der eine Zahl ergibt, wählt diesen Ordinalzahlenknoten aus. Beispielsweise gibt der Speicherortpfad `Customer[3]` den dritten Kunden zurück. Solche numerische Prädikate werden nicht unterstützt. Nur Prädikatausdrücke, die ein boolesches Ergebnis zurückgeben, werden unterstützt.  
  
> [!NOTE]  
>  Informationen zu den Einschränkungen dieser XPath-Implementierung von XPath und die Unterschiede zwischen ihm und der W3C-Spezifikation finden Sie unter [Einführung in XPath-Abfragen mithilfe von &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="selection-predicate-example-1"></a>Auswahlprädikat: Beispiel 1  
 Der folgende XPath-Ausdruck (Speicherortpfad) Wählt alle aktuellen Kontextknotens aus der  **\<Kunden >** -Element untergeordneten der **CustomerID** Attribut mit dem Wert ALFKI:  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 In dieser XPath-Abfrage sind `child` und `attribute` die Achsennamen. `Customer` ist der Knotentest (TRUE, wenn `Customer` ist ein  **\<Elementknoten >**, da  **\<Element >** ist der Hauptknotentyp für die `child` Achse). `attribute::CustomerID="ALFKI"` ist das Prädikat. Im Prädikat ist `attribute` ist die Achse und `CustomerID` ist der Knotentest (TRUE, wenn **CustomerID** ist ein Attribut des Kontextknotens aus, da  **\<Attribut >** ist der Prinzipal Knotentyp **Attribut** Achse).  
  
 In abgekürzter Syntax kann die XPath-Abfrage auch wie folgt angegeben werden:  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>Auswahlprädikat: Beispiel 2  
 Der folgende XPath-Ausdruck (Speicherortpfad) Wählt alle aktuellen Kontextknotens aus der  **\<Reihenfolge >** untergeordneten Knoten zweiter Ordnung, denen die **SalesOrderID** Attribut mit dem Wert 1:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 In diesem XPath-Ausdruck sind `child` und `attribute` die Achsennamen. `Customer`, `Order` und `SalesOrderID` sind die Knotentests. `attribute::OrderID="1"` ist das Prädikat.  
  
 In abgekürzter Syntax kann die XPath-Abfrage auch wie folgt angegeben werden:  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>Auswahlprädikat: Beispiel 3  
 Der folgende XPath-Ausdruck (Speicherortpfad) Wählt alle aktuellen Kontextknotens aus der  **\<Kunden >** untergeordnete Elemente, die eine mehrere oder  **\<ContactName >** untergeordnete Elemente:  
  
```  
child::Customer[child::ContactName]  
```  
  
 In diesem Beispiel wird vorausgesetzt, dass die  **\<ContactName >** ist ein untergeordnetes Element von der  **\<Kunden >** Element in der XML-Dokument, das so genannte  *elementzentrierte Zuordnung* in einem XSD-Schema mit Anmerkungen.  
  
 In diesem XPath-Ausdruck ist `child` der Achsenname. `Customer` ist der Knotentest (TRUE, wenn `Customer` ist ein  **\<Element >** Knoten, da  **\<Element >** ist der Hauptknotentyp für `child` Achse). `child::ContactName` ist das Prädikat. Im Prädikat ist `child` ist die Achse und `ContactName` ist der Knotentest (TRUE, wenn `ContactName` ist ein  **\<Element >** Knoten).  
  
 Dieser Ausdruck gibt nur die  **\<Kunden >** -Element untergeordneten Knoten des Kontextknotens  **\<ContactName >** Element untergeordnete Elemente.  
  
 In abgekürzter Syntax kann die XPath-Abfrage auch wie folgt angegeben werden:  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>Auswahlprädikat: Beispiel 4  
 Der folgende XPath-Ausdruck wählt  **\<Kunden >** -Elemente des Kontextknotens, auf denen kein  **\<ContactName >** untergeordneten Elemente:  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 In diesem Beispiel wird vorausgesetzt, dass  **\<ContactName >** ist ein untergeordnetes Element von der  **\<Kunden >** Element in das XML-Dokument, das ContactName-Feld ist nicht erforderlich, der die Datenbank.  
  
 In diesem Beispiel ist `child` die Achse. `Customer` ist der Knotentest (TRUE, wenn `Customer` ist ein \<Element > Knoten). `not(child::ContactName)` ist das Prädikat. Im Prädikat ist `child` ist die Achse und `ContactName` ist der Knotentest (TRUE, wenn `ContactName` ist ein \<Element > Knoten).  
  
 In abgekürzter Syntax kann die XPath-Abfrage auch wie folgt angegeben werden:  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>Auswahlprädikat: Beispiel 5  
 Der folgende XPath-Ausdruck wählt alle aktuellen Kontextknotens aus der  **\<Kunden >** untergeordneten der **CustomerID** Attribut:  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 In diesem Beispiel `child` ist die Achse und `Customer` ist der Knotentest (TRUE, wenn `Customer` ist ein \<Element > Knoten). `attribute::CustomerID` ist das Prädikat. Im Prädikat ist `attribute` ist die Achse und `CustomerID` ist das Prädikat (TRUE, wenn `CustomerID` ist ein  **\<Attribut >** Knoten).  
  
 In abgekürzter Syntax kann die XPath-Abfrage auch wie folgt angegeben werden:  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>Auswahlprädikat: Beispiel 6  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 unterstützt XPath-Abfragen mit einem Kreuzprodukt im Prädikat, wie im folgenden Beispiel gezeigt:  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 Durch diese Abfrage werden alle Kunden mit einer `Order` ausgewählt, bei der `OrderDate` dem `ShipDate` für eine beliebige `Order`entspricht.  
  
## <a name="see-also"></a>Siehe auch  
 [Einführung in mit Anmerkungen versehene XSD-Schemas &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [Die clientseitige XML-Formatierung & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
