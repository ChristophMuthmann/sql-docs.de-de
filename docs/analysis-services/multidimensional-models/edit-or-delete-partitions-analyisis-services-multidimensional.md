---
title: "Bearbeiten oder Löschen von Partitionen (Analyisis Services – mehrdimensional) | Microsoft Docs"
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
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a253d7cc22d90a06369a914b7aec8b4a8ec315f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>Bearbeiten oder Löschen von Partitionen (Analyisis Services – Mehrdimensional)
  Cubepartitionen werden über die Registerkarte **Partitionen** im Cube-Designer von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]geändert. Auf der Registerkarte **Partitionen** werden die Partitionen für alle Measuregruppen in einem Cube aufgeführt. Ebenfalls werden die Rückschreibepartitionen mit aktiviertem Rückschreiben aufgeführt.  
  
 Um die Partitionen für eine beliebige Measuregruppe zu bearbeiten, erweitern Sie die Measuregruppe auf der Registerkarte **Partitionen** . Die Partitionen für eine Measuregruppe werden nach Ordnungszahl in einem Tabellenformat mit den in der folgenden Tabellen angegebenen Spalten aufgeführt.  
  
 Die Einstellungen für eine verknüpfte Measuregruppe müssen im Quellcube bearbeitet werden.  
  
 Das Löschen von Partitionen erfolgt automatisch, wenn Sie eine Quellpartition mit einer Zielpartition zusammenführen. Die als Quelle angegebene Partition wird nach Ende der Zusammenführung gelöscht. Sie können die Partitionen auch manuell in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder auf der Registerkarte Partitionen in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]löschen. Klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Löschen**aus. Zur Erinnerung: Beim Löschen einer Partition werden auch Daten und Aggregationen entfernt. Zur Vorsicht sollten Sie eine neuere Datenbanksicherung erstellen, falls Sie das Löschen später rückgängig machen müssen.  
  
> [!NOTE]  
>  Alternativ können Sie XMLA-Skripts verwenden, um die Erstellung, das Zusammenführen und das Löschen von Partitionen zu automatisieren. XMLA-Skripts können in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]oder in benutzerdefinierten SSIS-Paketen, die als geplanter Task ablaufen, erstellt und ausgeführt werden. Weitere Informationen finden Sie unter [Automate Analysis Services Administrative Tasks with SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="partition-source"></a>Partitionsquelle  
 Gibt die Quelltabelle oder benannte Abfrage für die Partition an. Klicken Sie auf die Zelle, und klicken Sie anschließend auf die Schaltfläche zum Durchsuchen (**...**), um die Quelltabelle zu ändern.  
  
 ![Quellspalte im Bereich "Partition"](../../analysis-services/multidimensional-models/media/ssas-partitionsource.png "Quellspalte im Bereich "Partition"")  
  
 Wenn die Partition auf einer Abfrage basiert, klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um die Abfrage zu bearbeiten. Dadurch wird die **Source** -Eigenschaft der Partition bearbeitet. Weitere Informationen finden Sie unter [Ändern einer Partitionsquelle für die Verwendung einer anderen Faktentabelle](../../analysis-services/multidimensional-models/change-a-partition-source-to-use-a-different-fact-table.md).  
  
 Sie können eine Tabelle in der Datenquellensicht angeben, die die gleiche Struktur wie die ursprüngliche Quelltabelle (in der externen Datenquelle, aus der die Daten abgerufen werden) aufweist. Bei der Quelle kann es sich um eine beliebige Datenquelle oder Datenquellensicht der Cubedatenbank handeln.  
  
## <a name="storage-settings"></a>Speichereinstellungen  
 Im Cube-Designer auf der Registerkarte Partitionen können Sie auf **Speichereinstellungen** klicken, um eine der Standardeinstellungen für MOLAP-, ROLAP- oder HOLAP-Speicher auszuwählen, oder um benutzerdefinierte Einstellungen für den Speichermodus und das proaktive Zwischenspeichern zu konfigurieren. Die Standardmethode ist MOLAP, da sie die schnellste Abfrageleistung bietet. Weitere Informationen zu den einzelnen Einstellungen finden Sie unter [Festlegen des Partitionsspeichers &#40;Analysis Services – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md).  
  
 Speicher kann für jede Partition einer einzelnen Measuregruppe eines Cubes separat konfiguriert werden. Sie können auch die Standardspeichereinstellungen für einen Cube oder für eine Measuregruppe konfigurieren. Der Speicher wird im Cube-Assistenten auf der Registerkarte **Partitionen** konfiguriert.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten einer lokalen Partition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)   
 [Entwerfen von Aggregationen &#40; Analysis Services – mehrdimensional &#41;](../../analysis-services/multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)   
 [Zusammenführen von Partitionen in Analysis Services &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
