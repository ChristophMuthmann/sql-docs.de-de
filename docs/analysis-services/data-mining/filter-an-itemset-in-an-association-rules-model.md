---
title: Filtern eines Itemset in einem Zuordnungsmodell | Microsoft Docs
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
- itemsets [Analysis Services]
- filtering itemsets [Analysis Services]
- Mining Model Viewer [Analysis Services], itemsets
ms.assetid: 3ed919ea-8598-45d2-a4a0-b1b3357a4ab1
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bb07516c57e5364e92ee1efe249efb0cbd8bbefb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="filter-an-itemset-in-an-association-rules-model"></a>Filtern eines Itemset in einem Zuordnungsregelmodell
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]können Sie die Itemsets filtern, die auf der Registerkarte **Itemsets** des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Viewers angezeigt werden.  
  
### <a name="to-filter-an-itemset"></a>So filtern Sie ein Itemset  
  
1.  Klicken Sie auf der Registerkarte **Miningmodell-Viewer** des Data Mining-Designers in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf die Registerkarte **Itemsets** des **Zuordnungsregel-Viewers**.  
  
2.  Geben Sie in das Feld **Filteritemset** eine Regelbedingung ein. Eine Regelbedingung könnte z. B. "Touring-1000 = existing" sein.  
  
3.  Klicken Sie auf **Eingabe**.  
  
 Die Itemsets werden jetzt gefiltert und zeigen nur die Itemsets an, die die ausgewählten Elemente enthalten. In diesem Feld wird nicht nach Groß-/Kleinschreibung unterschieden. Filter werden im Arbeitsspeicher gespeichert. Sie können daher einen alten Filter aus der Liste auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodell-Viewer miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
