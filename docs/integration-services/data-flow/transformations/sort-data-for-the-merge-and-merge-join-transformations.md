---
title: "Sortieren von Daten für die Zusammenführung und Merge Join Transformationen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sort attributes [Integration Services]
- output columns [Integration Services]
ms.assetid: 22ce3f5d-8a88-4423-92c2-60a8f82cd4fd
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b9a99a414a74e873e5c09d22c6469a13ac04a32d
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sort-data-for-the-merge-and-merge-join-transformations"></a>Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin
  In [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]erfordern die Transformationen für Zusammenführen und Zusammenführungsjoin sortierte Daten für ihre Eingaben. Die Eingabedaten müssen physisch sortiert werden, und die Sortierungsoptionen müssen für die Ausgaben und die Ausgabespalten in der Quelle oder Upstreamtransformation festgelegt werden. Wenn die Sortierungsoptionen anzeigen, dass die Daten sortiert sind, dies jedoch in Wirklichkeit nicht der Fall ist, sind die Ergebnisse des Vorgangs der Zusammenführung oder des Zusammenführungsjoins nicht vorhersagbar.  
  
## <a name="sorting-the-data"></a>Sortieren der Daten  
 Sie können diese Daten auch mithilfe einer der folgenden Methoden sortieren:  
  
-   Verwenden Sie in der Quelle eine ORDER BY-Klausel in der Anweisung, die zum Laden der Daten verwendet wird.  
  
-   Fügen Sie im Datenfluss vor der Transformation für Zusammenführung oder dem Zusammenführungsjoin eine Transformation zum Sortieren ein.  
  
 Wenn es sich bei den Daten um Zeichenfolgendaten handelt, erwartet sowohl die Transformation für Zusammenführung als auch die für den Zusammenführungsjoin, dass die Zeichenfolgenwerte mithilfe der Windows-Sortierung sortiert wurden. Führen Sie die folgenden Vorgänge aus, um Zeichenfolgenwerte für die Transformationen für Zusammenführung und für den Zusammenführungsjoin bereitzustellen, die mithilfe der Windows-Sortierung sortiert wurden.  
  
#### <a name="to-provide-string-values-that-are-sorted-by-using-windows-collation"></a>So stellen Sie mithilfe der Windows-Sortierung sortierte Zeichenfolgenwerte bereit  
  
-   Sortieren Sie die Daten mit einer Transformation zum Sortieren.  
  
     Die Transformation zum Sortieren verwendet die Windows-Sortierung, um Zeichenfolgenwerte zu sortieren.  
  
     – oder –  
  
-   Verwenden Sie den Transact-SQL-Umwandlungsoperator (CAST), um die **varchar** -Werte zuerst in **nvarchar** -Werte umzuwandeln, und sortieren Sie die Daten anschließend mit der ORDER BY-Klausel in Transact-SQL.  
  
    > [!IMPORTANT]  
    >  Die ORDER BY-Klausel allein reicht nicht aus, da sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Sortierung zum Sortieren der Zeichenfolgenwerte verwendet. Mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Sortierung ergibt sich möglicherweise eine andere Sortierreihenfolge als mit der Windows-Sortierung. Dadurch könnte die Transformation für Zusammenführung und für Zusammenführungsjoin zu unerwarteten Ergebnissen führen.  
  
## <a name="setting-sort-options-on-the-data"></a>Festlegen von Sortieroptionen für die Daten  
 Es gibt zwei wichtige Sortiereigenschaften, die für die Quelle oder die Upstreamtransformation festgelegt werden müssen, die die Daten für Transformationen für Zusammenführen und für Zusammenführungsjoin bereitstellen.  
  
-   Die **IsSorted** -Eigenschaft der Ausgabe, die angibt, ob die Daten sortiert wurden. Diese Eigenschaft muss auf **True**festgelegt werden.  
  
    > [!IMPORTANT]  
    >  Durch die Festlegung des Werts für die Eigenschaft **IsSorted** auf **True** werden keine Daten sortiert. Diese Eigenschaft ist lediglich ein Hinweis für die Downstreamkomponenten, dass die Daten vorher sortiert wurden.  
  
-   Die **SortKeyPosition** -Eigenschaft der Ausgabespalten, die angibt, ob eine Spalte sortiert ist sowie die Sortierreihenfolge der Spalte und die Sequenz, in der mehrere Spalten sortiert wurden. Diese Eigenschaft muss für jede Spalte sortierter Daten festgelegt werden.  
  
 Wenn Sie zum Sortieren der Daten eine Transformation zum Sortieren verwenden, legt die Transformation zum Sortieren diese beiden von der Transformation für Zusammenführen und für Zusammenführungsjoin verlangten Eigenschaften fest. Das heißt, die Transformation zum Sortieren legt die **IsSorted** -Eigenschaft ihrer Ausgabe auf **True**fest und legt die **SortKeyPosition** -Eigenschaften ihrer Ausgabespalten fest.  
  
 Wenn Sie zum Sortieren der Daten jedoch keine Transformation zum Sortieren verwenden, müssen Sie diese Sortiereigenschaften für die Quelle oder die Upstreamtransformation manuell festlegen. Verwenden Sie folgendes Verfahren, um die Sortiereigenschaften für die Quelle oder Upstreamtransformation manuell festzulegen.  
  
#### <a name="to-manually-set-sort-attributes-on-a-source-or-transformation-component"></a>So legen Sie Sortierattribute für eine Quelle oder Transformationskomponente manuell fest  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Suchen Sie auf der Registerkarte **Datenfluss** nach der entsprechenden Quelle oder Upstreamtransformation, oder ziehen Sie diese von der **Toolbox** auf die Entwurfsoberfläche.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Komponente, und klicken Sie auf **Erweiterten Editor anzeigen**.  
  
5.  Klicken Sie auf die Registerkarte **Eingabe- und Ausgabeeigenschaften** .  
  
6.  Klicken Sie auf  **\<Komponentenname > Ausgabe**, und legen Sie die **IsSorted** Eigenschaft **"true"**.  
  
    > [!NOTE]  
    >  Wenn Sie die **IsSorted** -Eigenschaft der Ausgabe manuell auf **True** festlegen und die Daten nicht sortiert sind, kann es beim Ausführen des Pakets in der Downstreamtransformation für Zusammenführung oder des Zusammenführungsjoins zu Vergleichsvorgängen mit fehlenden oder beschädigten Daten kommen.  
  
7.  Erweitern Sie **Ausgabespalten**.  
  
8.  Klicken Sie auf die Spalte, die Sie als sortiert kennzeichnen möchten, und legen Sie für die **SortKeyPosition** -Eigenschaft einen ganzzahligen Wert ungleich 0 fest. Beachten Sie dabei folgende Hinweise:  
  
    -   Der ganzzahlige Wert muss eine numerische Sequenz darstellen, die bei 1 beginnt und sich jeweils um 1 erhöht.  
  
    -   Ein positiver ganzzahliger Wert gibt eine aufsteigende Sortierreihenfolge an.  
  
    -   Ein negativer ganzzahliger Wert gibt eine absteigende Sortierreihenfolge an. (Wenn eine negative Zahl angegeben wird, legt der absolute Wert der Zahl die Position der Spalte in der Sortierreihenfolge fest.)  
  
    -   Der Standardwert 0 gibt an, dass die Spalte nicht sortiert ist. Lassen Sie den Wert 0 für Ausgabespalten unverändert, die kein Bestandteil der Sortierung sind.  
  
     Beachten Sie als Beispiel für die Festlegung der **SortKeyPosition** -Eigenschaft folgende Transact-SQL-Anweisung, die Daten in eine Quelle lädt:  
  
     `SELECT * FROM MyTable ORDER BY ColumnA, ColumnB DESC, ColumnC`  
  
     Für diese Anweisung würden Sie die **SortKeyPosition** -Eigenschaft für jede Spalte folgendermaßen festlegen:  
  
    -   Legen Sie die **SortKeyPosition** -Eigenschaft von ColumnA auf 1 fest. Dies gibt an, dass ColumnA die erste Spalte ist, die sortiert wird, und dass sie in aufsteigender Reihenfolge sortiert wird.  
  
    -   Legen Sie die **SortKeyPosition** -Eigenschaft von ColumnB auf -2 fest. Dies gibt an, dass ColumnB die zweite Spalte ist, die sortiert wird, und dass sie in absteigender Reihenfolge sortiert wird.  
  
    -   Legen Sie die **SortKeyPosition** -Eigenschaft von ColumnC auf 3 fest. Dies gibt an, dass ColumnC die dritte Spalte ist, die sortiert wird, und dass sie in aufsteigender Reihenfolge sortiert wird.  
  
9. Wiederholen Sie Schritt 8 für jede sortierte Spalte.  
  
10. Klicken Sie auf **OK**.  
  
11. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für zusammenführen](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  
