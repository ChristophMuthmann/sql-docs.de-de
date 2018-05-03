---
title: Drillthrough zu Falldaten aus einem Miningmodell | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ef80f8e442bf5950af6b955324e7dcca8f9d84e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>Ausführen von Drillthroughs für Falldaten aus einem Miningmodell
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
>  Einige Modelle können keinen Drillthrough verwenden. Die Möglichkeit eines Drillthrough hängt von dem für die Erstellung des Modells verwendeten Algorithmus ab. Eine Liste der Miningmodelltypen, die Drillthrough unterstützen, finden Sie unter [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>So zeigen Sie Drillthroughdaten von einem Miningmodell an  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]die Miningstruktur, die das gewünschte Miningmodell enthält.  
  
2.  Klicken Sie im Data Mining-Designer auf die Registerkarte **Miningmodell-Viewer** .  
  
3.  Wählen Sie das Modell aus der Dropdownliste **Miningmodell** aus.  
  
4.  Wählen Sie einen Viewer aus der Dropdownliste **Viewer** aus, und klicken Sie mit der rechten Maustaste auf den entsprechenden Knoten.  
  
5.  Wählen Sie **Drillthrough**und anschließend entweder **Nur Modellspalten**oder **Modell- und Strukturspalten** , um das Fenster **Drillthrough** zu öffnen.  
  
6.  Um die Daten in die Zwischenablage zu kopieren, klicken Sie mit der rechten Maustaste auf eine beliebige Zeile in der Tabelle, und wählen Sie **Alle kopieren**.  
  
## <a name="see-also"></a>Siehe auch  
 [Drillthroughabfragen & #40; Datamining & #41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  
