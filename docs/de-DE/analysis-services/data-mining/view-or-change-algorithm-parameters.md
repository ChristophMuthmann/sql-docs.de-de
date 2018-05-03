---
title: Anzeigen oder Ändern von Algorithmusparametern | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services], algorithms
ms.assetid: 151b899b-c27a-4a09-bcf5-5c9f0ec24168
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7f4fa6cce6be014857a94a0f78c863adaf091cc6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="view-or-change-algorithm-parameters"></a>Anzeigen oder Ändern von Algorithmusparametern
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sie können die Parameter ändern, die mit den Algorithmen zum Erstellen von Data Mining-Modellen bereitgestellt wurden, um die Ergebnisse des Modells anzupassen.  
  
 Durch die in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellten Algorithmusparameter wird viel mehr als nur die Eigenschaften des Modells geändert. Sie können auch verwendet werden, um die Methode, mit der Daten verarbeitet, gruppiert und angezeigt werden, grundlegend zu ändern. Sie können mithilfe von Algorithmusparametern beispielsweise Folgende Aufgaben ausführen:  
  
-   Ändern der Analysemethode, z. B. die Clustermethode.  
  
-   Steuern des Funktionsauswahlverhaltens.  
  
-   Angeben der Größe von Itemsets oder der Wahrscheinlichkeit von Regeln.  
  
-   Steuern der Elementverzweigung und der Tiefe von Entscheidungsstrukturen.  
  
-   Angeben eines Ausgangswert oder der Größe des internen zur Modellerstellung verwendeten Zurückhaltungsdatasets.  
  
 Die für jeden Algorithmus bereitgestellten Parameter variieren stark. Eine Liste der Parameter, die Sie für jeden Algorithmus festlegen können, finden Sie in den technische Referenzthemen in folgendem Abschnitt: [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="change-an-algorithm-parameter"></a>Ändern eines Algorithmusparameters  
  
1.  Klicken Sie in der Registerkarte **Miningmodelle** des Data Mining-Designers in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]mit der rechten Maustaste auf den Algorithmustyp des Miningmodells, dessen Algorithmus Sie optimieren wollen, und klicken Sie anschließend auf **Algorithmusparameter festlegen**.  
  
     Das Dialogfeld **Algorithmusparameter** wird geöffnet.  
  
2.  Legen Sie in der **Wert** -Spalte einen neuen Wert für den Algorithmus fest, den Sie ändern wollen.  
  
     Wenn Sie in die **Wert** -Spalte keinen Wert eingeben, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den Standardparameterwert. Die **Bereich** -Spalte beschreibt die möglichen Eingabewerte.  
  
3.  Klicken Sie auf **OK**.  
  
     Der Algorithmusparameter wird auf den neuen Wert festgelegt. Die Parameteränderung wird erst dann im Miningmodell widergespiegelt, wenn Sie das Modell erneut verarbeitet haben.  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>Anzeigen der in einem vorhandenen Modell verwendeten Parameter  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ein DMX-Abfragefenster in.  
  
2.  Geben Sie eine ähnliche Abfrage wie die Folgende ein:  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
