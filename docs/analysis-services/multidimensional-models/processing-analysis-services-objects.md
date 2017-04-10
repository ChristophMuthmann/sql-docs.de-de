---
title: "Verarbeiten von Analysis Services-Objekten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OLAP-Objekte [Analysis Services], verarbeiten"
  - "OLAP-Objekte [Analysis Services]"
ms.assetid: c7e1f66f-16ca-43da-b8c7-4d3e1fa8b58d
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# Verarbeiten von Analysis Services-Objekten
  Die Verarbeitung betrifft die folgenden [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekttypen: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken, -Cubes, -Dimensionen, -Measuregruppen, -Partitionen, -Miningmodelle und -Miningstrukturen. Sie können für jedes der Objekte eine Verarbeitungsstufe angeben, oder Sie können die Option Standard verarbeiten angeben, um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die automatische Auswahl der optimalen Verarbeitungsstufe zu überlassen. Weitere Informationen zu den verschiedenen Ebenen zum Verarbeiten aller Objekte finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 Es ist wichtig, dass Sie sich der möglichen Konsequenzen des Verarbeitungsverhaltens bewusst sind, um eventuelle negative Auswirkungen zu vermeiden. Wenn Sie zum Beispiel die vollständige Verarbeitung einer Dimension wählen, werden alle von dieser Dimension abhängigen Partitionen in den Status 'Nicht verarbeitet' versetzt. Davon betroffene Cubes sind dann nicht für Abfragen verfügbar, bis die abhängigen Partitionen verarbeitet sind.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Verarbeiten einer Datenbank](#bkmk_procdb)  
  
 [Verarbeiten einer Dimension](#bkmk_procdim)  
  
 [Verarbeiten eines Cube](#bkmk_proccube)  
  
 [Verarbeiten einer Measuregruppe](#bkmk_procmeasure)  
  
 [Verarbeiten einer Partition](#bkmk_procpartition)  
  
 [Verarbeiten von Data Mining-Strukturen und -Modellen](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> Verarbeiten einer Datenbank  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]enthält eine Datenbank Objekte, aber keine Daten. Wenn Sie eine Datenbank verarbeiten, weisen Sie den Server an, jene Objekte, die Daten im Modell speichern, z. B. Dimensionen, Partitionen, Miningstrukturen und Miningmodelle, rekursiv zu verarbeiten.  
  
 Beim Verarbeiten einer Datenbank werden einige oder alle der in der Datenbank enthaltenen Partitionen, Dimensionen und Miningmodelle verarbeitet. Der Verarbeitungstyp hängt vom Status der einzelnen Objekte und von den von Ihnen ausgewählten Verarbeitungsoptionen ab. Weitere Informationen finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
##  <a name="bkmk_proccube"></a> Verarbeiten eines Cube  
 Sie können sich einen Cube als ein Wrapperobjekt für Measuregruppen und Partitionen vorstellen. Ein Cube setzt sich aus Dimensionen sowie aus mindestens einem Measure zusammen, welche in Partitionen gespeichert werden. Dimensionen definieren die Ausrichtung der Daten im Cube. Beim Verarbeiten eines Cubes wird eine SQL-Abfrage ausgegeben, um Werte aus den Faktentabellen abzurufen, um so jedes Cubeelement mit den jeweils geeigneten Measurewerten aufzufüllen. Für jeden bestimmten Pfad zu einem Cubeknoten ist ein Wert oder ein berechenbarer Wert vorhanden.  
  
 Bei der Cubeverarbeitung verarbeitet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle unverarbeiteten Dimensionen des Cubes und bestimmte oder alle der in den Measuregruppen des Cubes enthaltenen Partitionen. Die genaueren Umstände der Verarbeitung hängen sowohl vom Zustand der Objekte bei Verarbeitungsbeginn als auch von den Verarbeitungsoptionen ab, die Sie ausgewählt haben. Weitere Informationen zu Verarbeitungsoptionen finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 Beim Verarbeiten eines Cubes entstehen maschinenlesbare Dateien, in denen relevante Faktendaten gespeichert sind. Falls Aggregationen erstellt werden, werden diese in Aggregationsdatendateien gespeichert. Der Cube kann anschließend im Objekt-Explorer von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder im Projektmappen-Explorer von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> Verarbeiten einer Dimension  
 Bei der Verarbeitung einer Dimension formuliert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Abfragen und führt diese aus; die Abfragen geben dann die für die Verarbeitung benötigten Informationen aus den Dimensionstabellen zurück.  
  
|Country|Verkaufsregion|Status|  
|-------------|------------------|-----------|  
|USA|West|California|  
|USA|West|Oregon|  
|USA|West|Washington|  
  
 Die Verarbeitung selbst wandelt die tabellarischen Daten in verwendbare Hierarchien um. Diese Hierarchien sind vollständig angezeigte Elementnamen und werden intern durch eindeutige numerische Pfade dargestellt. Das folgende Beispiel ist eine Textdarstellung einer Hierarchie.  
  
||  
|-|  
|[USA]|  
|[USA].[West]|  
|[USA].[West].[California]|  
|[USA].[West].[Oregon]|  
|[USA].[West].[Washington]|  
  
 Bei der Dimensionsverarbeitung werden keine auf Cubeebene definierten berechneten Elemente erstellt oder aktualisiert. Die berechneten Elemente werden beim Update der Cubedefinition berücksichtigt. Bei der Dimensionsverarbeitung werden auch keine Aggregationen erstellt oder aktualisiert. Die Dimensionsverarbeitung kann jedoch verursachen, dass Aggregationen gelöscht werden. Aggregationen werden ausschließlich während der Verarbeitung von Partitionen erstellt oder aktualisiert.  
  
 Beim Verarbeiten einer Dimension ist zu beachten, dass die Dimension eventuell in mehreren Cubes verwendet wird. Wenn Sie eine Dimension verarbeiten, werden diese Cubes als unverarbeitet markiert und sind nicht mehr für Abfragen verfügbar. Um sowohl die Dimension als auch die damit verbundenen Cubes zur gleichen Zeit zu verarbeiten, sollten Sie entsprechende Stapelverarbeitungseinstellungen verwenden. Weitere Informationen finden Sie unter [Batchverarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md).  
  
##  <a name="bkmk_procmeasure"></a> Verarbeiten einer Measuregruppe  
 Beim Verarbeiten einer Measuregruppe verarbeitet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bestimmte oder alle Partitionen in der Measuregruppe und alle unverarbeiteten Dimensionen, die Teil der Measuregruppe sind. Die Einzelheiten des Verarbeitungsauftrags hängen davon ab, welche Verarbeitungsoptionen Sie ausgewählt haben. Sie können eine oder mehrere Measuregruppen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verarbeiten, ohne dass sich dies auf andere Measuregruppen eines Cubes auswirkt.  
  
> [!NOTE]  
>  Die Verarbeitung einzelner Measuregruppen kann programmgesteuert oder mithilfe von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]erfolgen. Einzelne Measuregruppen können Sie nur in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]verarbeiten, wenn dies partitionsweise geschieht.  
  
##  <a name="bkmk_procpartition"></a> Verarbeiten einer Partition  
 Die effiziente Verwaltung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beinhaltet das geübte Partitionieren von Daten. Bei der Partitionsverarbeitung müssen Sie die Festplattenverwendung und Speicherplatzeinschränkungen sowie die durch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]vorgegebenen Datenstrukturbeschränkungen berücksichtigen. Sie müssen Partitionen regelmäßig erstellen, verarbeiten und zusammenführen, um schnelle Abfrageantwortzeiten und einen hohen Verarbeitungsdurchsatz sicherzustellen. Äußerst wichtig ist außerdem, dass Sie sich der Gefahr bewusst sind, dass sich bei der Zusammenführung von Partitionen redundante Daten einschleichen können, um effizient dagegen vorgehen zu können. Weitere Informationen finden Sie unter [Zusammenführen von Partitionen in Analysis Services &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
 Wenn Sie eine Partition verarbeiten, verarbeitet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Partition und alle darin vorhandenen unverarbeiteten Dimensionen in Abhängigkeit der Verarbeitungsoptionen, die Sie ausgewählt haben. Das Verwenden von Partitionen bringt für die Verarbeitung eine Reihe von Vorteilen mit sich. Sie können eine Partition verarbeiten, ohne dass sich dies auf andere Partitionen eines Cubes auswirkt. Partitionen sind besonders hilfreich beim Speichern von Daten, bei denen ein Zellenrückschreiben stattfindet. Beim Rückschreiben handelt es sich um eine Funktion, die dem Benutzer das Ausführen von Was-wäre-wenn-Analysen ermöglicht. Dabei werden neue Daten in die Partition zurückgeschrieben, um die projizierten Änderungen zu betrachten. Für den Einsatz der Rückschreibefunktion von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist eine Rückschreibepartition erforderlich. Es empfiehlt sich die parallele Verarbeitung von Partitionen, da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in diesem Fall eine effizientere Verarbeitungsleistung erreichen und die Gesamtverarbeitungszeit erheblich reduzieren kann. Partitionen können auch sequenziell verarbeitet werden.  
  
##  <a name="bkmk_procdm"></a> Verarbeiten von Data Mining-Strukturen und -Modellen  
 Eine Miningstruktur definiert die Datendomäne, aus der die Data Mining-Modelle erstellt werden. Eine Miningstruktur kann mehr als ein Miningmodell enthalten. Eine Miningstruktur kann separat von den zugeordneten Miningmodellen verarbeitet werden. Wenn Sie eine Miningstruktur separat verarbeiten, wird diese mit den Trainingsdaten Ihrer Datenquelle aufgefüllt.  
  
 Wenn ein Data Mining-Modell verarbeitet wird, werden die Trainingsdaten an den Miningmodellalgorithmus übergeben. Dabei wird das Miningmodell mithilfe des Data Mining-Algorithmus trainiert und der Inhalt aufgebaut. Weitere Informationen zum Datamining-Modellobjekt finden Sie unter [Miningstrukturen &#40;Analysis Services – Datamining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 Weitere Informationen zum Verarbeiten von Miningstrukturen und -modellen finden Sie unter [Anforderungen und Überlegungen zur Verarbeitung &#40;Data Mining&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
## Siehe auch  
 [Tools und Ansätze für die Verarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [Batchverarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)   
 [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  