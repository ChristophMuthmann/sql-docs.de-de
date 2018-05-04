---
title: Cube-Speicher (Analysis Services – mehrdimensionale Daten) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 942974dd2aff1c6286e66125eb23fe4dda9a866b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cube-storage-analysis-services---multidimensional-data"></a>Cubespeicherung (Analysis Services – Mehrdimensionale Daten)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Der Speicher kann nur Cubemetadaten oder alle Quelldaten aus der Faktentabelle sowie die Aggregationen enthalten, die durch Dimensionen im Bezug auf die Measuregruppe definiert sind. Die gespeicherte Datenmenge hängt vom ausgewählten Speichermodus und der Anzahl der Aggregationen ab. Die Abfrageleistung ist abhängig vom Umfang der direkt gespeicherten Daten. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] minimiert den erforderlichen Speicherplatz für Cubedaten und Aggregationen mithilfe verschiedener Verfahren:  
  
-   Mithilfe von Speicheroptionen können Sie die Speichermodi und Speicherorte auswählen, die für Cubedaten am besten geeignet sind.  
  
-   Ein hoch entwickelter Algorithmus entwirft effektive Zusammenfassungsaggregationen, um den erforderlichen Speicher zu minimieren, ohne die Geschwindigkeit zu beeinträchtigen.  
  
-   Für leere Zellen wird kein Speicherplatz zugeordnet.  
  
 Der Speicher wird für einzelne Partitionen definiert. Für jede Measuregruppe in einem Cube ist mindestens eine Partition vorhanden. Weitere Informationen finden Sie unter [Partitionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md), [Partition Speichermodi und Verarbeitung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [Measures und Measuregruppen](../../analysis-services/multidimensional-models/measures-and-measure-groups.md), und [Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md).  
  
## <a name="partition-storage"></a>Partition Storage  
 Der Speicher für eine Measuregruppe kann in mehrere Partitionen unterteilt werden. Mithilfe von Partitionen können Sie eine Measuregruppe in unterschiedlichen Segmenten auf einem oder mehreren Servern verteilen und Speicher und Abfrageleistung optimieren. Jede Partition in einer Measuregruppe kann auf einer anderen Datenquelle basieren und mit anderen Speichereinstellungen gespeichert werden.  
  
 Sie legen die Datenquelle für eine Partition fest, wenn Sie sie erstellen. Sie können die Datenquelle für eine vorhandene Partition auch ändern. Eine Measuregruppe kann vertikal oder horizontal partitioniert werden. Jede Partition in einer vertikal partitionierten Measuregruppe basiert auf der gefilterten Sicht einer einzelnen Quelltabelle. Wenn eine Measuregruppe beispielsweise auf einer einzelnen Tabelle mit mehreren Jahren an Daten basiert, können Sie eine separate Partition für die Daten der einzelnen Jahre erstellen. Im Gegensatz dazu basiert jede Partition in einer horizontal partitionierten Measuregruppe auf einer separaten Tabelle. Horizontale Partitionen sollten Sie verwenden, wenn die Datenquelle die Daten der einzelnen Jahre jeweils in einer separaten Tabelle speichert.  
  
 Partitionen werden zunächst mit denselben Speichereinstellungen erstellt wie die Measuregruppe, in der sie erstellt werden. Die Speichereinstellungen bestimmen, ob die Detail- und Aggregationsdaten im mehrdimensionalen Format auf der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], im relationalen Format auf dem Quellserver oder in einer Kombination aus beidem gespeichert werden. Speichereinstellungen bestimmen außerdem, ob proaktives Zwischenspeichern verwendet wird, um automatisch an die mehrdimensionalen Daten auf quelldatenänderungen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Die Partitionen eines Cubes sind für den Benutzer nicht sichtbar. Allerdings kann die Auswahl von Speichereinstellungen für verschiedene Partitionen sich auf die Unmittelbarkeit von Daten, den erforderlichen Speicherplatz und die Abfrageleistung auswirken. Partitionen können auf mehreren Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gespeichert werden. Dies bietet bei der Cubespeicherung eine Art Clustering und verteilt die Arbeitsauslastung auf die Server mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Weitere Informationen finden Sie unter [Partition Speichermodi und Verarbeitung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [Remotepartitionen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md), und [Partitionen &#40;Analysis Services – mehrdimensionale Daten&#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md).  
  
## <a name="linked-measure-groups"></a>Verknüpfte Measuregruppen  
 Die Speicherung mehrerer Kopien eines Cubes auf verschiedenen Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] kann viel Speicherplatz beanspruchen, der erforderliche Speicherplatz lässt sich jedoch bedeutend reduzieren, indem Sie Kopien einer Measuregruppe durch verknüpfte Measuregruppen ersetzen. Eine verknüpfte Measuregruppe basiert auf einer Measuregruppe in einem Cube in einer anderen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank auf demselben oder auf eine andere Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Verknüpfte Measuregruppen können auch mit verknüpften Dimensionen aus demselben Quellcube verwendet werden. Die verknüpften Dimensionen und Measuregruppen verwenden die Aggregationen des Quellcubes und besitzen keine eigenen Datenspeicheranforderungen. Durch das Verwalten von Quellmeasuregruppen und Dimensionen in einer Datenbank und das Erstellen verknüpfter Cubes und Dimensionen in Cubes in anderen Datenbanken können Sie sehr viel Speicherplatz sparen. Weitere Informationen finden Sie unter [Linked Measure Groups](../../analysis-services/multidimensional-models/linked-measure-groups.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Aggregationen und Aggregationsentwürfe](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
