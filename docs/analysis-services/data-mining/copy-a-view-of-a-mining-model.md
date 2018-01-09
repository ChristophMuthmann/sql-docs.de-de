---
title: Kopieren einer Sicht eines Miningmodells | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clipboards [data mining]
- Mining Model Viewer [Analysis Services], clipboards
- copying mining models to clipboard
ms.assetid: 768372db-e5b4-4990-b459-03d854fd9a6d
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c1b439df2696fc44552d42680e1d4642e4728aa9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="copy-a-view-of-a-mining-model"></a>Kopieren einer Sicht eines Miningmodells
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die **Miningmodell-Viewer** Registerkarte Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] wird Sie für jeden Typ von Miningmodell einen separater Viewer verwendet. Einige der Viewer weisen Komponenten auf, aus denen der Inhalt in die Zwischenablage kopiert und von dort in ein Dokument oder eine Bildbearbeitungssoftware eingefügt werden kann. Folgende Komponenten stellen diese Funktionalität zur Verfügung:  
  
-   Clusterdiagramm im Cluster-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)] und im Sequenzcluster-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Entscheidungsstruktur im Struktur-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)] und im Zeitreihe-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Statusübergänge im Sequenzcluster-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Abhängigkeitsnetzwerk im Zuordnungsregeln-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)] , Viewer für naives Bayes-Verfahren von [!INCLUDE[msCoName](../../includes/msconame-md.md)] und Struktur-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Miningmodellinhalt, im Bereich Knotendetails des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewers  
  
 Sie können die gesamte Darstellung des Miningmodells oder nur den im Viewer sichtbaren Teil kopieren.  
  
> [!WARNING]  
>  Wenn Sie mit dem Viewer ein Modell kopieren, wird kein neues Modellobjekt erstellt. Um ein neues Modell zu erstellen, müssen Sie entweder den Assistenten oder den Data Mining-Designer verwenden. Weitere Informationen finden Sie unter [Erstellen einer Kopie eines Miningmodells](../../analysis-services/data-mining/make-a-copy-of-a-mining-model.md).  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>So kopieren Sie das gesamte Modell in die Zwischenablage  
  
1.  Wählen Sie in der Liste **Miningmodell** auf der Registerkarte **Miningmodell-Viewer** das Miningmodell aus, das angezeigt werden soll.  
  
2.  Wählen Sie die entsprechende Registerkarte aus, beispielsweise die Registerkarte **Abhängigkeitsnetzwerk** , und klicken Sie dann auf der Symbolleiste dieser Registerkarte auf **Gesamtes Diagramm kopieren** .  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>So kopieren Sie den sichtbaren Teil des Modells in die Zwischenablage  
  
1.  Wählen Sie in der Liste **Miningmodell** auf der Registerkarte **Miningmodell-Viewer** das Miningmodell aus, das angezeigt werden soll.  
  
2.  Wählen Sie die entsprechende Registerkarte aus, beispielsweise die Registerkarte **Abhängigkeitsnetzwerk** , und vergrößern bzw. verkleinern Sie die Darstellung dann entsprechend, um das Modell in dem von Ihnen gewünschten Umfang anzuzeigen.  
  
3.  Klicken Sie auf der Symbolleiste der ausgewählten Registerkarte auf **Diagrammsicht kopieren** .  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>So kopieren Sie den Inhalt des Miningmodells in die Zwischenablage  
  
1.  Wählen Sie in der Liste **Miningmodell** auf der Registerkarte **Miningmodell-Viewer** das Miningmodell aus, das angezeigt werden soll.  
  
2.  Wählen Sie in der Dropdownliste **Viewer** die Option **Microsoft Generic Content Tree Viewer**aus.  
  
3.  Klicken Sie im Bereich **Knotenbeschriftung (eindeutige ID)** auf einen Knoten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Bereich **Knotendetails** , und wählen Sie **Alles auswählen**aus.  
  
5.  Klicken Sie mit der rechten Maustaste erneut auf den Bereich **Knotendetails** , und wählen Sie **Kopieren**aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Tasks und Anweisungen für den Miningmodell-Viewer](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
