---
title: AMO-OLAP-Klassen | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: 397509b7-a4fb-40de-aa30-c66dc9ed2105
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ef144b4a141c15d9d84f4e3e226f654a8f4feff
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="amo-olap-classes"></a>AMO-OLAP-Klassen
  OLAP-Klassen in Analysis Management Objects (AMO) erleichtern das Erstellen, Bearbeiten, Löschen und Verarbeiten von Cubes, Dimensionen und verknüpften Objekten wie Key Performance Indicators (KPIs), Aktionen und proaktiver Zwischenspeicherung.  
  
 Weitere Informationen zum Einrichten der AMO-Programmierumgebung wie zum Herstellen einer Verbindung mit einem Server, den Zugriff auf eine Datenbank oder zum Definieren von Datenquellen und Datenquellensichten finden Sie unter [grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Dimensionsobjekte](#Dimensions)  
  
-   [Cubeobjekte](#Cubes)  
  
-   [MeasureGroup-Objekte](#MeasureGroups)  
  
-   [Partitionsobjekte](#Partition)  
  
-   [AggregationDesign-Objekte](#AggregationDesign)  
  
-   [Aggregationsobjekte](#Aggregation)  
  
-   [Aktionsobjekte](#Action)  
  
-   [KPI-Objekte](#KPI)  
  
-   [Perspective-Objekte](#Perspective)  
  
-   [Übersetzungsobjekte](#Translation)  
  
-   [ProactiveCaching-Objekte](#ProactiveCaching)  
  
 Die folgende Abbildung zeigt die Beziehung der in diesem Thema erläuterten Klassen.  
  
 ![OLAP-Klassen in AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-olapclasses.gif "OLAP-Klassen in AMO")  
  
## <a name="basic-classes"></a>Grundlegende Klassen  
  
###  <a name="Dimensions"></a>Dimensionsobjekte  
 Eine Dimension wird erstellt, indem sie der Dimensionsauflistung der übergeordneten Datenbank hinzugefügt und das <xref:Microsoft.AnalysisServices.Dimension>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird.  
  
 Um eine Dimension zu entfernen, müssen Sie sie mithilfe der Drop-Methode der <xref:Microsoft.AnalysisServices.Dimension> löschen. Entfernen einer <xref:Microsoft.AnalysisServices.Dimension> aus den Dimensionen-Auflistung der Datenbank mithilfe der Remove-Methode löscht keine es auf dem Server nur im AMO-Objektmodell.  
  
 Ein <xref:Microsoft.AnalysisServices.Dimension> Objekt verarbeitet werden kann, nachdem es erstellt wurde. Die <xref:Microsoft.AnalysisServices.Dimension> kann mithilfe ihrer eigenen Verarbeitungsmethode verarbeitet werden, oder sie kann mithilfe der Verarbeitungsmethode des übergeordneten Objekts verarbeitet werden, wenn das übergeordnete Objekt verarbeitet wird.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Dimension> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Cubes"></a>Cubeobjekte  
 Ein Cube wird erstellt, indem er der Cubeauflistung der Datenbank hinzugefügt und das <xref:Microsoft.AnalysisServices.Cube>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird. Die Update-Methode des Cubes kann den Parameter UpdateOptions.ExpandFull enthalten, der sicherstellt, dass alle geänderten Objekte im Cube im Rahmen dieses Updatevorgangs auf dem Server aktualisiert werden.  
  
 Um einen Cube zu entfernen, muss er gelöscht werden, indem Sie mit der Drop-Methode, der die <xref:Microsoft.AnalysisServices.Cube>. Wenn ein Cube aus der Auflistung entfernt wird, wirkt sich dies nicht auf den Server aus.  
  
 Ein <xref:Microsoft.AnalysisServices.Cube> Objekt verarbeitet werden kann, nachdem es erstellt wurde. Die <xref:Microsoft.AnalysisServices.Cube> kann mithilfe seiner eigenen Verarbeitungsmethode verarbeitet werden, oder sie kann verarbeitet werden, wenn ein übergeordnetes Objekt selbst mit seiner eigenen Verarbeitungsmethode verarbeitet.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Cube> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="MeasureGroups"></a>MeasureGroup-Objekte  
 Eine Measuregruppe wird erstellt, indem sie der Measuregruppenauflistung des Cubes hinzugefügt und anschließend das <xref:Microsoft.AnalysisServices.MeasureGroup>-Objekt mithilfe seiner eigenen Update-Methode auf dem Server aktualisiert wird. Ein <xref:Microsoft.AnalysisServices.MeasureGroup>-Objekt wird mit seiner eigenen Drop-Methode entfernt.  
  
 Ein <xref:Microsoft.AnalysisServices.MeasureGroup> Objekt verarbeitet werden kann, nachdem es erstellt wurde. Die <xref:Microsoft.AnalysisServices.MeasureGroup> mithilfe seiner eigenen Verarbeitungsmethode verarbeitet werden können, oder sie kann verarbeitet werden, wenn ein übergeordnetes Objekt selbst mit seiner eigenen Verarbeitungsmethode verarbeitet.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.MeasureGroup> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Partition"></a>Partitionsobjekte  
 Ein <xref:Microsoft.AnalysisServices.Partition> Objekt wird erstellt, indem es der partitionsauflistung der übergeordneten Measuregruppe hinzugefügt und anschließend die <xref:Microsoft.AnalysisServices.Partition> Objekt auf dem Server mithilfe der Update-Methode. Ein <xref:Microsoft.AnalysisServices.Partition>-Objekt wird mithilfe der Drop-Methode entfernt.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Partition> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="AggregationDesign"></a>AggregationDesign-Objekte  
 Aggregationsentwürfe werden erstellt, mit der AggregationDesign-Methode aus einer <xref:Microsoft.AnalysisServices.AggregationDesign> Objekt.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.AggregationDesign> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Aggregation"></a>Aggregationsobjekte  
 Ein <xref:Microsoft.AnalysisServices.Aggregation>-Objekt wird erstellt, indem es der Auflistung der Aggregationsentwürfe der übergeordneten Measuregruppe hinzugefügt und anschließend das übergeordnete Measuregruppenobjekt mithilfe der Update-Methode auf dem Server aktualisiert wird. Eine Aggregation wird mit der Remove-Methode oder der RemoveAt-Methode aus der <xref:Microsoft.AnalysisServices.AggregationCollection> entfernt.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Aggregation> in der <xref:Microsoft.AnalysisServices>.  
  
## <a name="advanced-classes"></a>Erweiterte Klassen  
 Erweiterte Klassen stellen OLAP-Funktionalität bereit, die über das Erstellen und Durchsuchen eines Cubes hinausgeht. Im Folgenden sind einige der erweiterten Klassen und ihre Vorteile aufgelistet:  
  
-   Aktionsklassen werden verwendet, um beim Durchsuchen von bestimmten Bereichen des Cubes eine aktive Antwort zu erstellen.  
  
-   Key Performance Indicators (KPIs) aktivieren die Vergleichsanalyse zwischen Datenwerten.  
  
-   Perspektiven bieten ausgewählte Sichten eines einzelnen Cubes, sodass Benutzer sich auf die für sie wichtigen Aspekte konzentrieren können.  
  
-   Übersetzungen ermöglichen es dem Cube, an das Benutzergebietsschema angepasst zu werden.  
  
-   Die Klassen für das proaktive Zwischenspeichern ermöglichen ein Gleichgewicht zwischen der verbesserten Leistung der MOLAP-Speicherung und der Unmittelbarkeit der ROLAP-Speicherung und bieten eine Partitionsverarbeitung basierend auf einem festgelegten Zeitplan.  
  
 AMO wird zum Festlegen der Definitionen für dieses verbesserte Verhalten verwendet. Das eigentliche Verhalten wird jedoch vom Browsing-Client definiert, der alle diese Verbesserungen implementiert.  
  
###  <a name="Action"></a>Aktionsobjekte  
 Ein <xref:Microsoft.AnalysisServices.Action>-Objekt wird erstellt, indem es der Auflistung der Aktionen des Cubes hinzugefügt und anschließend das <xref:Microsoft.AnalysisServices.Cube>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird. Die Update-Methode des Cubes kann den Parameter UpdateOptions.ExpandFull enthalten, der sicherstellt, dass alle geänderten Objekte im Cube im Rahmen dieses Updatevorgangs auf dem Server aktualisiert werden.  
  
 Um ein <xref:Microsoft.AnalysisServices.Action>-Objekt zu entfernen, müssen Sie es aus der Auflistung löschen und den übergeordneten Cube aktualisieren.  
  
 Ein Cube muss aktualisiert und verarbeitet werden, bevor die Aktion über den Client verwendet werden kann.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Action> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="KPI"></a>KPI-Objekte  
 Ein <xref:Microsoft.AnalysisServices.Kpi> Objekt wird erstellt, indem es der KPI-Auflistung des Cubes hinzugefügt und anschließend die <xref:Microsoft.AnalysisServices.Cube> -Objekt auf dem Server mithilfe der Update-Methode. Die Update-Methode des Cubes kann den Parameter UpdateOptions.ExpandFull enthalten, der sicherstellt, dass alle geänderten Objekte im Cube im Rahmen dieses Updatevorgangs auf dem Server aktualisiert werden.  
  
 So entfernen Sie eine <xref:Microsoft.AnalysisServices.Kpi> -Objekts können sie muss aus der Auflistung entfernt werden und der übergeordneten Cube muss aktualisiert werden.  
  
 Ein Cube muss aktualisiert und verarbeitet werden, bevor der KPI verwendet werden kann.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Kpi> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Perspective"></a>Perspective-Objekte  
 Ein <xref:Microsoft.AnalysisServices.Perspective>-Objekt wird erstellt, indem es der Perspektivenauflistung des Cubes hinzugefügt und anschließend das <xref:Microsoft.AnalysisServices.Cube>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird. Die Update-Methode des Cubes kann den Parameter UpdateOptions.ExpandFull enthalten, der sicherstellt, dass alle geänderten Objekte im Cube im Rahmen dieses Updatevorgangs auf dem Server aktualisiert werden.  
  
 Um ein <xref:Microsoft.AnalysisServices.Perspective>-Objekt zu entfernen, müssen Sie es aus der Auflistung löschen und dann den übergeordneten Cube aktualisieren.  
  
 Ein Cube muss aktualisiert und verarbeitet werden, bevor die Perspektive verwendet werden kann.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Perspective> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Translation"></a>Übersetzungsobjekte  
 Ein <xref:Microsoft.AnalysisServices.Translation>-Objekt wird erstellt, indem es der Übersetzungsauflistung des gewünschten Objekts hinzugefügt und anschließend das am nächsten liegende übergeordnete Hauptobjekt mithilfe der Update-Methode auf dem Server aktualisiert wird. Die Update-Methode des am nächsten liegenden übergeordneten Objekts kann den Parameter UpdateOptions.ExpandFull enthalten, der sicherstellt, dass alle untergeordneten geänderten Objekte im Rahmen dieses Updatevorgangs auf dem Server aktualisiert werden.  
  
 So entfernen Sie ein <xref:Microsoft.AnalysisServices.Translation> -Objekt muss aus der Auflistung entfernt werden, und klicken Sie dann den nächste übergeordneten Objekt muss aktualisiert werden.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Translation> in der <xref:Microsoft.AnalysisServices>.  
  
###  <a name="ProactiveCaching"></a>ProactiveCaching-Objekte  
 Ein <xref:Microsoft.AnalysisServices.ProactiveCaching> Objekt wird erstellt, indem es die proaktive Zwischenspeicherung objektauflistung der Dimension oder Partition hinzugefügt, dann aktualisieren die Dimension oder Partition-Objekt an den Server mithilfe der Update-Methode.  
  
 So entfernen Sie eine <xref:Microsoft.AnalysisServices.ProactiveCaching> Objekt ist, muss Sie aus der Auflistung entfernt werden, und klicken Sie dann das übergeordnete Objekt muss aktualisiert werden.  
  
 Eine Dimension oder Partition muss aktualisiert und verarbeitet werden, bevor die proaktive Zwischenspeicherung aktiviert und einsatzbereit ist.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.ProactiveCaching> in der <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programmieren AMO OLAP Basic-Objekten](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md)   
 [Programmieren AMO-OLAP-von erweiterten Objekten](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

