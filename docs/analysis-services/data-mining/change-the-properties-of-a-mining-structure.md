---
title: "Ändern der Eigenschaften einer Miningstruktur | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], properties
ms.assetid: 03b16897-2e36-42b8-9f7d-db1b9b898401
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 908bf89105dbcfc4c61a4018c92a8cee71237fb9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="change-the-properties-of-a-mining-structure"></a>Ändern der Eigenschaften einer Miningstruktur
  Es gibt zwei Arten von Eigenschaften in einer Miningstruktur, die jeweils geändert werden können:  
  
-   Eigenschaften der Miningstruktur, die die gesamte Struktur betreffen.  
  
-   Eigenschaften in einzelnen Spalten in der Struktur  
  
 Einige Eigenschaften sind von anderen Eigenschafteneinstellungen abhängig. Sie können beispielsweise keine Eigenschaften festlegen, die das Diskretisierungsverhalten steuern (wie <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> oder <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>), solange Sie den Datentyp der Spalte auf **Diskretisiert**festgelegt haben.  
  
 Weitere Informationen zu Miningstruktureigenschaften finden Sie unter [Miningstrukturspalten](../../analysis-services/data-mining/mining-structure-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-structure"></a>So ändern Sie die Eigenschaften einer Miningstruktur  
  
1.  Klicken Sie auf der Registerkarte **Miningstruktur** im Data Mining-Designer mit der rechten Maustaste entweder auf die Miningstruktur oder auf eine Spalte innerhalb der Miningstruktur, und klicken Sie anschließend auf **Eigenschaften**.  
  
     Im rechten Bildschirmbereich wird das **Eigenschaften** -Fenster geöffnet, wenn es nicht bereits sichtbar war.  
  
2.  Wählen Sie im **Eigenschaften** -Fenster den Wert aus, der der Eigenschaft entspricht, die Sie ändern möchten, und geben Sie dann den neuen Wert ein.  
  
     Der neue Wert wird wirksam, wenn Sie ein anderes Element im Designer auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

