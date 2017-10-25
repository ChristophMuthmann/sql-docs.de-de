---
title: "Verarbeiten von Partitionen in der Arbeitsbereichsdatenbank (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 650821073c8c2c15d143ba0fb2ff24e1352c9cb6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="process-partitions-in-the-workspace-databse-ssas-tabular"></a>Verarbeiten von Partitionen in der Arbeitsbereichsdatenbank (SSAS – tabellarisch)
  Durch Partitionen wird eine Tabelle logisch unterteilt. Jede Partition kann unabhängig von anderen Partitionen verarbeitet (aktualisiert) werden. In den Tasks in diesem Thema wird beschrieben, wie Partitionen in der Arbeitsbereichsdatenbank des Modells in **mithilfe des Dialogfelds** Partitionen verarbeiten [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verarbeitet werden.  
  
 Nachdem ein Modell in einer anderen Analysis Services-Instanz bereitgestellt wurde, können Datenbankadministratoren Partitionen im (bereitgestellten) Modell mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], mittels eines Skripts oder unter Verwendung eines IS-Pakets erstellen und verwalten. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Tabellenmodellpartitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
###  <a name="bkmk_create_new"></a> So verarbeiten Sie eine Partition  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im Modell-Designer auf das Menü **Modell** , auf **Verarbeiten** (Aktualisieren) und anschließend auf **Partitionen verarbeiten**.  
  
2.  Wählen Sie im Listenfeld **Modus** einen der folgenden Verarbeitungsmodi aus:  
  
    |Modus|Description|  
    |----------|-----------------|  
    |**Standard verarbeiten**|Erkennt den Verarbeitungsstatus eines Partitionsobjekts und führt die Verarbeitung durch, durch die nicht oder teilweise verarbeitete Partitionsobjekte in den Status "Vollständig verarbeitet" versetzt werden. Daten für leere Tabellen und Partitionen werden geladen, Hierarchien, berechnete Spalten und Beziehungen werden erstellt oder neu erstellt.|  
    |**Vollständig verarbeiten**|Verarbeitet ein Partitionsobjekt und alle darin enthaltenen Objekte. Wenn die Verarbeitungsmethode "Vollständig verarbeiten" für ein bereits verarbeitetes Objekt ausgeführt wird, löscht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Daten im Objekt und verarbeitet anschließend das Objekt. Diese Art der Verarbeitung ist erforderlich, wenn eine Änderung an der Objektstruktur vorgenommen wurde.|  
    |**Daten verarbeiten**|Lädt Daten in eine Partition oder Tabelle, ohne Hierarchien oder Beziehungen neu zu erstellen bzw. berechnete Spalten und Measures neu zu berechnen.|  
    |**Löschung verarbeiten**|Entfernt alle Daten aus einer Partition.|  
    |**Hinzufügung verarbeiten**|Aktualisiert die Partition inkrementell mit neuen Daten.|  
  
3.  Wählen Sie in der Spalte der Kontrollkästchen unter **Verarbeiten** die Partitionen aus, die im ausgewählten Modus verarbeitet werden sollen, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Erstellen und Verwalten von Partitionen in der Arbeitsbereichsdatenbank &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  

