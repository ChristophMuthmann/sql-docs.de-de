---
title: Drillthrough zu Falldaten aus einem Miningmodell | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drillthrough [Analysis Services]
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 849c244bdfb40770d8038a78a430faa7ff26b6b8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>Ausführen von Drillthroughs für Falldaten aus einem Miningmodell
  Wenn Sie in einem Miningmodell Drillthrough für die Modellfälle aktiviert haben, können Sie beim Durchsuchen des Modells detaillierte Informationen über die Fälle abrufen, die für die Erstellung des Modells verwendet wurden. Wenn in der zugrunde liegenden Miningstruktur ebenfalls Drillthrough für Strukturfälle aktiviert wurde und Sie über die entsprechenden Berechtigungen verfügen, können Sie Informationen aus der Miningstruktur zurückgeben. Dies kann Spalten einschließen, die nicht im Miningmodell enthalten sind.  
  
 Wenn die Miningstruktur keinen Drillthrough für die zugrunde liegenden Daten gestattet, jedoch das Miningmodell, können Sie nur Informationen der Modellfälle anzeigen, nicht jedoch der Miningstruktur.  
  
> [!NOTE]  
>  Sie können einem vorhandenen Miningmodell die Funktion für einen Drillthrough hinzufügen, indem Sie die **AllowDrillthrough** -Eigenschaft auf **True**festlegen. Nachdem Sie Drillthroughs aktiviert haben, muss das Modell jedoch erneut verarbeitet werden, bevor Sie die Falldaten anzeigen können. Weitere Informationen finden Sie unter [Aktivieren von Drillthrough für ein Miningmodell](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 In Abhängigkeit von dem verwendeten Viewer können Sie den Knoten für den Drillthrough folgendermaßen auswählen:  
  
|Name des Viewers|Name des Bereichs oder der Registerkarte|Knoten auswählen|  
|-----------------|----------------------|-----------------|  
|**Microsoft Struktur-Viewer**|Registerkarte**Entscheidungsstruktur** |Klicken Sie auf einen Strukturknoten.<br /><br /> **Hinweis** Führen Sie nach Möglichkeit keinen Drillthrough auf dem **All** -Knoten aus, da es sehr lange dauern kann, bis Ergebnisse zurückgegeben werden.|  
|**Microsoft Cluster-Viewer**|**Clusterdiagramm**|Klicken Sie auf einen Clusterknoten.|  
|**Microsoft Cluster-Viewer**|**Clusterprofile**|Klicken Sie auf eine beliebige Stelle in der Clusterspalte.|  
|**Microsoft Association Rules-Viewer**|Registerkarte**Regeln** |Klicken Sie auf eine Zeile, die einen Satz von Regeln enthält.|  
|**Microsoft Association Rules-Viewer**|Registerkarte**Itemsets** |Klicken Sie auf eine Zeile, die ein Itemset enthält.|  
|**Microsoft Sequence Cluster-Viewer**|Registerkarte**Regeln** |Klicken Sie auf eine Zeile, die einen Satz von Regeln enthält.|  
|**Microsoft Sequence Cluster-Viewer**|Registerkarte**Itemsets** |Klicken Sie auf eine Zeile, die ein Itemset enthält.|  
  
> [!NOTE]  
>  Einige Modelle können keinen Drillthrough verwenden. Die Möglichkeit eines Drillthrough hängt von dem für die Erstellung des Modells verwendeten Algorithmus ab. Eine Liste der Miningmodelltypen, die Drillthrough unterstützen, finden Sie unter [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)festlegen.  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>So zeigen Sie Drillthroughdaten von einem Miningmodell an  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]die Miningstruktur, die das gewünschte Miningmodell enthält.  
  
2.  Klicken Sie im Data Mining-Designer auf die Registerkarte **Miningmodell-Viewer** .  
  
3.  Wählen Sie das Modell aus der Dropdownliste **Miningmodell** aus.  
  
4.  Wählen Sie einen Viewer aus der Dropdownliste **Viewer** aus, und klicken Sie mit der rechten Maustaste auf den entsprechenden Knoten.  
  
5.  Wählen Sie **Drillthrough**und anschließend entweder **Nur Modellspalten**oder **Modell- und Strukturspalten** , um das Fenster **Drillthrough** zu öffnen.  
  
6.  Um die Daten in die Zwischenablage zu kopieren, klicken Sie mit der rechten Maustaste auf eine beliebige Zeile in der Tabelle, und wählen Sie **Alle kopieren**.  
  
## <a name="see-also"></a>Siehe auch  
 [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  

