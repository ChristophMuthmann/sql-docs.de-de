---
title: Erstellen und Verwalten einer lokalen Partition (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- local partitions [Analysis Services]
- partitions [Analysis Services], local
- partitions [Analysis Services], creating
ms.assetid: eaa95278-9ce9-47d5-a6b6-1046e7076599
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebc3093a0e030aca329338359be2a6f256c24fe7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-manage-a-local-partition-analysis-services"></a>Erstellen und Verwalten einer lokalen Partition (Analysis Services)
  Sie können zusätzliche Partitionen für eine Measuregruppe erstellen, um die Verarbeitungsleistung zu verbessern. Durch die Verwendung mehrerer Partitionen können Sie Faktendaten einer entsprechenden Anzahl physischer Datendateien sowohl auf lokalen als auch auf Remoteservern zuordnen. Da Partitionen in Analysis Services unabhängig und parallel verarbeitet werden können, erhalten Sie eine bessere Kontrolle über die Arbeitsauslastungen auf dem Server.  
  
 Partitionen können in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] während des Modellentwurfs oder nach der Bereitstellung der Projektmappe mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder XMLA erstellt werden. Es empfiehlt sich, nur einen von beiden Ansätzen zu nutzen. Wenn Sie zwischen den Tools wechseln, kann es vorkommen, dass die an einer bereitgestellten Datenbank in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] vorgenommenen Änderungen überschrieben werden, wenn die Projektmappe anschließend mithilfe von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]erneut bereitgestellt wird.  
  
## <a name="before-you-start"></a>Vorbereitungen  
 Überprüfen Sie, ob Sie die Business Intelligence Edition oder Enterprise Edition verwenden. Die Standard Edition bietet keine Unterstützung für mehrere Partitionen. Um die Edition festzustellen, klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit der rechten Maustaste auf den Serverknoten, und wählen Sie **Berichte** | **Allgemein**aus. Weitere Informationen zu den verfügbaren Funktionen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
 Zu Beginn sollten Sie wissen, dass Partitionen denselben Aggregationsentwurf aufweisen müssen, falls Sie sie später zusammenführen möchten. Partitionen können nur zusammengeführt werden, wenn sie über denselben Aggregationsentwurf und Speichermodus verfügen.  
  
> [!TIP]  
>  Überprüfen Sie die zu partitionierenden Daten in der Datenquellensicht (Data Source View, DSV), um einen Eindruck von Datenbereich und -tiefe zu erhalten. Wenn Sie z. B. nach dem Datum partitionieren, können Sie eine Sortierung nach einer Datumsspalte vornehmen, um die Ober- und Untergrenze der einzelnen Partitionen zu bestimmen.  
  
## <a name="choose-an-approach"></a>Auswählen eines Ansatzes  
 Der wichtigste Faktor beim Erstellen von Partitionen besteht darin, die Daten so zu segmentieren, dass keine doppelten Zeilen vorkommen. Die Daten dürfen jeweils nur in einer Partition enthalten sein, damit keine Zeilen doppelt gezählt werden. Aus diesem Grund wird häufig nach DATE partitioniert, sodass eindeutige Grenzen zwischen den einzelnen Partitionen definiert werden können.  
  
 Zum Verteilen der Faktendaten auf mehrere Partitionen können beide Verfahren eingesetzt werden. Folgende Verfahren können zum Segmentieren der Daten verwendet werden.  
  
|Verfahren|Empfehlungen|  
|---------------|---------------------|  
|Segmentieren von Faktendaten mithilfe von SQL-Abfragen|Partitionen können mithilfe von SQL-Abfragen definiert werden. Während der Verarbeitung werden die Daten mit der SQL-Abfrage abgerufen. In der WHERE-Klausel der Abfrage ist der Filter angegeben, durch den die Daten für die einzelnen Partitionen segmentiert werden. Die Abfrage wird von Analysis Services generiert, sodass Sie nur noch die WHERE-Klausel definieren müssen, um die Daten ordnungsgemäß zu segmentieren.<br /><br /> Der Hauptvorteil dieses Ansatzes besteht in der Leichtigkeit, mit der Daten aus einer einzelnen Quelltabelle partitioniert werden können. Wenn sämtliche Quelldaten aus einer umfangreichen Faktentabelle stammen, können Sie Filterabfragen erstellen, durch die die Daten in diskrete Partitionen aufgeteilt werden, ohne zusätzliche Datenstrukturen in der Datenquellensicht erzeugen zu müssen.<br /><br /> Ein Nachteil besteht darin, dass durch die Verwendung von Abfragen die Bindung zwischen Partition und DSV verloren geht. Wenn Sie die DSV später im Analysis Services-Projekt aktualisieren, indem Sie der Faktentabelle z. B. Spalten hinzufügen, müssen Sie die Abfragen für jede Partition manuell bearbeiten, damit die neue Spalte berücksichtigt wird. Für den zweiten Ansatz, der im Folgenden erläutert wird, gilt dieser Nachteil nicht.|  
|Segmentieren von Faktendaten mithilfe von Tabellen in der DSV|Sie können eine Partition an eine Tabelle, benannte Abfrage oder Sicht in der DSV binden. Als Ausgangsbasis für eine Partition sind die drei Ansätze funktionell gleichwertig. Die gesamte Tabelle, benannte Abfrage oder Sicht stellt sämtliche Daten für eine einzelne Partition bereit.<br /><br /> Bei Verwendung einer Tabelle, Sicht oder benannten Abfrage ist die gesamte Logik zur Datenauswahl in der DSV enthalten, die längerfristig einfacher zu verwalten und zu pflegen ist. Ein wichtiger Vorteil dieses Ansatzes besteht darin, dass die Tabellenbindungen erhalten bleiben. Wenn Sie die Quelltabelle später aktualisieren, müssen die Partitionen, die auf der Tabelle basieren, nicht geändert werden. Da alle Tabellen, benannten Abfragen und Sichten außerdem in einem gemeinsamen Arbeitsbereich enthalten sind, lassen sie sich wesentlich einfacher aktualisieren als Partitionsabfragen, die einzeln geöffnet und bearbeitet werden müssen.|  
  
## <a name="option-1-filter-a-fact-table-for-multiple-partitions"></a>Option 1: Filtern einer Faktentabelle für mehrere Partitionen  
 Um mehrere Partitionen zu erstellen, ändern Sie zunächst die **Source** -Eigenschaft der Standardpartition. Standardmäßig wird eine Measuregruppe unter Verwendung einer einzelnen Partition erstellt, die an genau eine Tabelle in der DSV gebunden ist. Da die ursprüngliche Partition nur einen Teil der Faktendaten enthalten soll, müssen Sie sie zunächst bearbeiten, bevor Sie weitere Partitionen hinzufügen können. Anschließend können Sie zusätzliche Partitionen erstellen, um die übrigen Daten darauf zu speichern.  
  
 Die Filter sollten so konzipiert sein, dass keine Daten zwischen Partitionen dupliziert werden. Der Filter einer Partition gibt an, welche Daten in der Faktentabelle in der Partition verwendet werden. Es ist wichtig, dass die Filter für alle Partitionen in einem Cube sich gegenseitig ausschließende Datasets aus der Faktentabelle extrahieren. Falls dieselben Faktendaten in mehreren Partitionen enthalten sind, könnten sie doppelt gezählt werden.  
  
1.  Doppelklicken Sie im Projektmappen-Explorer von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf den Cube, um ihn im Cube-Designer zu öffnen, und klicken Sie dann auf die Registerkarte **Partitionen** .  
  
2.  Erweitern Sie die Measuregruppe, für die Partitionen hinzugefügt werden. Standardmäßig verfügt jede Measuregruppe über eine Partition, die an eine Faktentabelle in der DSV gebunden ist.  
  
3.  Klicken Sie in der Quellspalte auf die Schaltfläche zum Durchsuchen (. .), um das Dialogfeld Partitionsquelle zu öffnen.  
  
     ![Quellspalte im Bereich "Partition"](../../analysis-services/multidimensional-models/media/ssas-partitionsource.png "Quellspalte im Bereich "Partition"")  
  
4.  Wählen Sie unter Bindungstyp die Option **Abfragebindung**aus. Die SQL-Abfrage zur Auswahl der Daten wird automatisch eingeblendet.  
  
5.  Fügen Sie in der WHERE-Klausel im unteren Bereich einen Filter hinzu, durch den die Daten für diese Partitionen segmentiert werden.  
  
     Beispiele für die Syntax von WHERE-Klauseln sind `WHERE OrderDateKey >= '20060101'` oder `WHERE OrderDateKey BETWEEN '20051001' AND '20051201'`. Weitere Beispiele finden Sie unter [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  
  
     Beachten Sie, dass sich die folgenden Filter innerhalb der einzelnen Sätze gegenseitig ausschließen:  
  
    |||  
    |-|-|  
    |Satz 1:|"SaleYear" = 2012<br /><br /> "SaleYear" = 2013|  
    |Satz 2:|"Continent" = 'NorthAmerica'<br /><br /> "Continent" = 'Europe'<br /><br /> "Continent" = 'SouthAmerica'|  
    |Satz 3:|"Country" = 'USA'<br /><br /> "Country" = 'Mexico'<br /><br /> ("Country" <> 'USA' AND "Country" <> 'Mexico')|  
  
6.  Klicken Sie auf **Überprüfen** , um Syntaxfehler zu suchen, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie die vorherigen Schritte, um die übrigen Partitionen zu erstellen. Ändern Sie dabei jeweils die WHERE-Klausel, damit der nächste Datenslice ausgewählt wird.  
  
8.  Stellen Sie die Projektmappe bereit, oder lassen Sie die Partition verarbeiten, um die Daten zu laden. Achten Sie darauf, dass alle Partitionen verarbeitet werden.  
  
9. Durchsuchen Sie den Cube, um sicherzustellen, dass die richtigen Daten zurückgegeben werden.  
  
 Nachdem Sie über eine Measuregruppe verfügen, die mehrere Measuregruppen verwendet, können Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zusätzliche Partitionen erstellen. Klicken Sie unterhalb einer Measuregruppe mit der rechten Maustaste auf den Ordner Partitionen, und wählen Sie **Neue Partitionen** aus, um den Assistenten zu starten.  
  
> [!NOTE]  
>  Anstatt Daten in einer Partition zu filtern, können Sie dieselbe Abfrage zum Erstellen einer benannten Abfrage in der DSV nutzen und dann die benannte Abfrage als Grundlage für die Partition verwenden.  
  
## <a name="option-2-use-tables-views-or-named-queries"></a>Option 2: Verwenden von Tabellen, Sichten oder benannten Abfragen  
 Wenn die Fakten in der DSV bereits in einzelne Tabellen unterteilt sind (beispielsweise nach Jahr oder Quartal), können Sie Partitionen auf Grundlage einer einzelnen Tabelle erstellen, wobei jede Partition über eine eigene Datenquellentabelle verfügt. Dies ist im Wesentlichen die Standardmethode zum Partitionieren von Measuregruppen. Bei mehreren Partitionen wird die ursprüngliche Partition jedoch in mehrere Partitionen aufgeteilt, wobei jede neue Partition der Datenquellentabelle zugeordnet wird, die die Daten bereitstellt.  
  
 Sichten und benannte Abfragen sind insofern mit Tabellen funktionell gleichwertig, dass alle drei Objekte in der DSV definiert werden und mithilfe der Option Tabellenbindung im Dialogfeld Partitionsquelle an eine Partition gebunden werden. Sie können eine Sicht oder benannte Abfrage erstellen, um das für jede Partition erforderliche Datensegment zu generieren. Weitere Informationen finden Sie unter [Definieren von benannten Abfragen in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md).  
  
> [!IMPORTANT]  
>  Wenn Sie für Partitionen in einer DSV benannte Abfragen erstellen, die sich gegenseitig ausschließen, sollten Sie sicherstellen, dass die kombinierten Partitionsdaten alle Daten aus einer Measuregruppe einschließen, die Sie in den Cube einbeziehen möchten. Vergewissern Sie sich, dass Sie keine Standardpartition belassen, die auf einer vollständigen Tabelle für eine Measuregruppe basiert. Andernfalls überlappen die Partitionen, die auf einer Abfrage basieren, die auf der vollständigen Tabelle basierende Abfrage.  
  
1.  Erstellen Sie mindestens eine benannte Abfrage, die als Partitionsquelle verwendet werden soll. Weitere Informationen finden Sie unter [Definieren von benannten Abfragen in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md).  
  
     Die benannte Abfrage muss auf der Faktentabelle basieren, die der Measuregruppe zugeordnet ist. Beispiel: Wenn Sie die FactInternetSales-Measuregruppe partitionieren, muss in der FROM-Anweisung der benannten Abfragen in der DSV die FactInternetSales-Tabelle angegeben sein.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf den Cube, um ihn im Cube-Designer zu öffnen, und klicken Sie dann auf die Registerkarte **Partitionen** .  
  
3.  Erweitern Sie die Measuregruppe, für die Partitionen hinzugefügt werden.  
  
4.  Klicken Sie auf **Neue Partition** , um den Partitions-Assistenten zu starten. Wenn Sie die benannten Abfragen unter Verwendung der an die Measuregruppe gebundenen Faktentabelle erstellt haben, sollte jede benannte Abfrage, die Sie im vorherigen Schritt erstellt haben, angezeigt werden.  
  
5.  Wählen Sie unter Quellinformationen angeben, eine der in einem vorherigen Schritt erstellten benannten Abfragen aus. Wenn keine benannten Abfragen angezeigt werden, wechseln Sie zurück zur DSV und überprüfen die FROM-Anweisung.  
  
6.  Klicken Sie auf **Weiter** , um auf den nachfolgenden Seiten die Standardwerte zu akzeptieren.  
  
7.  Geben Sie auf der letzten Seite mit dem Titel Assistenten abschließen einen aussagekräftigen Namen für die Partition an.  
  
8.  Klicken Sie auf **Fertig stellen**.  
  
9. Wiederholen Sie die vorherigen Schritte, um die übrigen Partitionen zu erstellen. Wählen Sie jedes Mal eine andere benannte Abfrage aus, um den nächsten Datenslice auszuwählen.  
  
10. Stellen Sie die Projektmappe bereit, oder lassen Sie die Partition verarbeiten, um die Daten zu laden. Achten Sie darauf, dass alle Partitionen verarbeitet werden.  
  
11. Durchsuchen Sie den Cube, um sicherzustellen, dass die richtigen Daten zurückgegeben werden.  
  
## <a name="next-step"></a>Nächster Schritt  
 Wenn Sie sich gegenseitig ausschließende Abfragen für Partitionen erstellen, sollten Sie sicherstellen, dass die kombinierten Partitionsdaten alle Daten einschließen, die Sie in den Cube einbeziehen möchten.  
  
 Im letzten Schritt sollte die Standardpartition, die auf der Tabelle selbst basiert war, normalerweise entfernt werden (falls sie noch vorhanden ist). Andernfalls überschneiden sich Abfragen, die auf den Partitionen basieren, mit Abfragen, die auf der gesamten Tabelle basieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Remotepartitionen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [Zusammenführen von Partitionen in Analysis Services &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  

