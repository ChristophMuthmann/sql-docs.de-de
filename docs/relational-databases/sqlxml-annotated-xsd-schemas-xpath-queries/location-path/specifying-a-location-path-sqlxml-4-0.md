---
title: Angeben eines Speicherortpfads (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f704e45b165ecb4e29d909bcce09f7af92fb0989
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Angeben eines Speicherortpfads (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XPath-Abfragen werden in Form eines Ausdrucks angegeben. Es gibt verschiedene Arten von Ausdrücken. Ein Speicherortpfad ist ein Ausdruck, der relativ zum Kontextknoten einen Satz von Knoten auswählt. Das Ergebnis der Auswertung eines Speicherortpfads ist ein Knotensatz.  
  
## <a name="types-of-location-paths"></a>Typen von Speicherortpfaden  
 Ein Speicherortpfad kann eine dieser beiden Formen haben:  
  
-   **Absoluter Speicherortpfad**  
  
     Ein absoluter Speicherortpfad beginnt am Stammknoten des Dokuments. Er besteht aus einem Schrägstrich (/) optional gefolgt von einem relativen Speicherortpfad. Der Schrägstrich (/) wählt den Stammknoten des Dokuments aus.  
  
-   **Relativer Speicherortpfad**  
  
     Ein relativer Speicherortpfad beginnt am Kontextknoten im Dokument. Ein Speicherortpfad besteht aus einer Folge von einem oder mehreren Positionsschritten, die durch einen Schrägstrich (/) getrennt sind. Jeder Schritt wählt relativ zum Kontextknoten einen Satz von Knoten aus. Die Anfangsschrittsequenz wählt relativ zu einem Kontextknoten einen Satz von Knoten aus. Jeder Knoten in diesem Satz wird als Kontextknoten für den folgenden Schritt verwendet. Die Knotensätze, die von diesem Schritt identifiziert werden, werden verknüpft. Z. B. **Child:: Order/Child:: OrderDetail** wählt die  **\<OrderDetail >** Element untergeordneten Elemente der  **\<Reihenfolge >** Element die untergeordneten Elemente des Kontextknotens.  
  
    > [!NOTE]  
    >  In der SQLXML 4.0-Implementierung von XPath beginnt jede XPath-Abfrage am Stammkontext, selbst wenn der XPath nicht ausdrücklich absolut ist. Zum Beispiel wird eine XPath-Abfrage, die mit "Customer" beginnt, als "/Customer" behandelt. In der XPath-Abfrage **Customer [Order]**, beginnt Customer am Stammkontext, Order jedoch am Customer-Kontext. Weitere Informationen finden Sie unter [Einführung in XPath-Abfragen mithilfe von &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Positionsschritte  
 Ein Speicherortpfad (absolut oder relativ) besteht aus Positionsschritten, die drei Teile enthalten:  
  
-   **Achse**  
  
     Die Achse gibt die Strukturbeziehung zwischen den vom Positionsschritt ausgewählten Knoten und dem Kontextknoten an. Die **übergeordneten**, **untergeordneten**, **Attribut**, und **self** Achsen werden unterstützt. Wenn eine **untergeordneten** angegebenen Achse im Speicherortpfad, alle von der Abfrage ausgewählten Knoten werden die untergeordneten Elemente des Kontextknotens. Wenn eine **übergeordneten** Achse angegeben wird, werden die ausgewählten Knoten ist der übergeordnete Knoten des Kontextknotens. Wenn ein **Attribut** Achse angegeben wird, sind die ausgewählten Knoten die Attribute des Kontextknotens.  
  
-   **Knotentest**  
  
     Ein Knotentest gibt den vom Positionsschritt ausgewählten Knotentyp an. Jede Achse (**untergeordneten**, **übergeordneten**, **Attribut**, und **self**) hat einen Hauptknotentyp. Für die **Attribut** Achse, der Hauptknotentyp ist  **\<Attribut >**. Für die **übergeordneten**, **untergeordneten**, und **self** Achsen, der Hauptknotentyp ist  **\<Element >**.  
  
     Beispielsweise im Speicherortpfad **Child:: Customer**,  **\<Kunden >** untergeordneten-Elemente des Kontextknotens ausgewählt sind. Da die **untergeordneten** Achse  **\<Element >** als Hauptknotentyp, ist der Knotentest Customer, "true", wenn Kunden eine  **\<Element >**Knoten.  
  
-   **Auswahlprädikate (null oder mehr)**  
  
     Ein Prädikat filtert einen Knotensatz in Bezug auf eine Achse. Die Angabe von Auswahlprädikaten in einem XPath-Ausdruck entspricht der Angabe einer WHERE-Klausel in einer SELECT-Anweisung. Das Prädikat wird zwischen Klammern angegeben. Wird der in den Auswahlprädikaten angegebene Test angewendet, werden die vom Knotentest zurückgegebenen Knoten gefiltert. Für jeden Knoten in der zu filternden Knotengruppe wird der Prädikatausdruck mit dem entsprechenden Knoten als Kontextknoten ausgewertet. Die Anzahl der Knoten in der Knotengruppe dient dabei als Kontextgröße. Ergibt die Auswertung des Prädikatausdrucks für den betreffenden Knoten TRUE, wird dieser Knoten in die resultierende Knotengruppe aufgenommen.  
  
     Die Syntax für einen Positionsschritt umfasst den Achsennamen und den Knotentest, getrennt durch zwei Doppelpunkte (::) und gefolgt von null oder mehr Ausdrücken in eckigen Klammern. Z. B. der XPath-Ausdruck (Speicherortpfad) **Child:: Customer [@CustomerID= "ALFKI"]** wählt alle dem  **\<Kunden >** untergeordneten-Elemente des Kontextknotens. Anschließend der Test im Prädikat auf den Knotensatz angewendet wird, die nur zurückgibt, die  **\<Kunden >** -Elementknoten mit dem Attribut-Wert 'ALFKI' für seine **CustomerID** Attribut.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Angeben einer Achse &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-an-axis-sqlxml-4-0.md)  
 Enthält Beispiele zur Angabe einer Achse.  
  
 [Angeben eines Knotentests in den Pfad zum Speicherort &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Enthält Beispiele zur Angabe eines Knotentests.  
  
 [Angeben von Auswahlprädikaten in den Pfad zum Speicherort &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/location-path/specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Enthält Beispiele zur Angabe von Auswahlprädikaten.  
  
  
