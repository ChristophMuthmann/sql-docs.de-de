---
title: Erstellen Sie eine Kopie eines Miningmodells | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
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
- mining models [Analysis Services], copying
- mining models [Analysis Services], creating
- mining models [Analysis Services], how-to topics
- copying mining models
ms.assetid: 7975bb02-f188-49a0-b7de-5b9b216254ad
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e8646d2de65b9dd2bd9fa0272a33b2cd4a5f0737
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="make-a-copy-of-a-mining-model"></a>Erstellen einer Kopie eines Miningmodells
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Erstellen eine Kopie eines Miningmodells eignet sich schnell mehrere Miningmodelle erstellen, die auf denselben Daten basieren. Nach dem Kopieren des Modells können Sie die neue Kopie bearbeiten, indem Sie Parameter ändern oder einen Filter hinzufügen.  
  
 Wenn Sie zum Beispiel eine Customers-Tabelle besitzen, die mit einer Tabelle verknüpft ist, in der Einkäufe aufgeführt sind, können Sie Kopien erstellen, um separate Miningmodelle für jede Kundendemografie zu generieren und nach Attributen wie Alter oder Region zu filtern.  
  
 Informationen zum Kopieren des Inhalts des Modells (z.B. die grafische Darstellung oder die Modellmuster) in die Zwischenablage zur Verwendung in anderen Programmen finden Sie unter [Kopieren einer Sicht eines Miningmodells](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md).  
  
### <a name="to-create-a-related-mining-model"></a>So erstellen Sie ein verknüpftes Miningmodell  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]in Projektmappen-Explorer auf die Miningstruktur, die das Miningmodell enthält.  
  
2.  Klicken Sie auf die Registerkarte **Miningmodelle** .  
  
3.  Wählen Sie das Modell aus, und klicken Sie mit der rechten Maustaste, um das Kontextmenü zu öffnen.  
  
     – Oder –  
  
     Wählen Sie das Modell aus. Klicken Sie im Menü **Miningmodell** auf **Neues Miningmodell**.  
  
4.  Geben Sie einen Namen für das neue Miningmodell ein, und wählen Sie einen Algorithmus aus. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>So bearbeiten Sie den Filter im kopierten Miningmodell  
  
1.  Wählen Sie das Miningmodell aus.  
  
2.  Klicken Sie im Fenster **Eigenschaften** auf das Textfeld für die **Filter** -Eigenschaft, und klicken Sie dann auf die Schaltfläche ( **…** ).  
  
3.  Ändern Sie die Filterbedingungen.  
  
     Weitere Informationen zur Verwendung der Dialogfelder des Filter-Editors finden Sie unter [Anwenden eines Filters auf ein Miningmodell](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
4.  Klicken Sie im Fenster **Eigenschaften** im Textfeld **AlgorithmParameters** auf **Algorithmusparameter festlegen**, und ändern Sie bei Bedarf Algorithmusparameter.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Löschen eines Filters aus einem Miningmodell](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
