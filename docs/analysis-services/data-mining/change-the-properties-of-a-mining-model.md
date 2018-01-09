---
title: "Ändern der Eigenschaften eines Miningmodells | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84259428c78b013577d50b6f48818bb2cd0dc554
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="change-the-properties-of-a-mining-model"></a>Ändern der Eigenschaften eines Miningmodells
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Einige miningmodelleigenschaften gelten für das Modell als Ganzes und andere Modelleigenschaften für einzelne Spalten gelten. Beispiele von Eigenschaften, die für das gesamte Modell gelten, sind die **Drillthrough** -Eigenschaft, die angibt, ob die Falldaten für Abfragen verfügbar sein sollen, und die **Description** -Eigenschaft. Eigenschaften, die für die Spalte gültig sind, schließen **Usage** und **ModelingFlags**ein, die steuern, wie Daten in der Spalte im Modell verwendet werden.  
  
 Die folgenden Modelleigenschaften besitzen erweiterte Editor-Programme, mit denen Ausdrücke erstellt oder komplexe Modelleigenschaften konfiguriert werden können. Funktionen der folgenden Eigenschaften:  
  
-   **Filter**-Eigenschaft: Öffnet das [Dialogfeld „Datasetfilter oder Modellfilter“](http://msdn.microsoft.com/library/a9602174-b7e2-4e16-8ded-dfd8eb9264d7).  
  
-   **AlgorithmParameters**-Eigenschaft: Öffnet das [Dialogfeld „Algorithmusparameter“ &#40;Miningmodelle-Sicht&#41;](http://msdn.microsoft.com/library/57f9f6f8-8ca4-4a6e-8f18-85f0571b7060).  
  
 Informationen zum Festlegen der Eigenschaften eines Miningmodells finden Sie unter [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>So ändern Sie die Eigenschaften eines Miningmodells  
  
1.  Klicken Sie im Data Mining-Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste entweder auf den Spaltenheader, der den Namen des Miningmodells enthält, oder auf die Zeile des Rasters mit dem Namen des Miningalgorithmus. Wählen Sie anschließend **Eigenschaften**aus.  
  
2.  Wählen Sie im Fenster **Eigenschaften** auf der rechten Seite des Bildschirms den Wert aus, der der Eigenschaft entspricht, die Sie ändern möchten, und geben Sie dann den neuen Wert ein.  
  
     Der neue Wert wird wirksam, wenn Sie ein anderes Element im Designer auswählen.  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>So ändern Sie die Eigenschaften einer Miningmodellspalte  
  
1.  Klicken Sie im Data Mining-Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste auf die Zelle des Rasters im Schnittpunkt zwischen Miningstrukturspalte und Miningmodell. Wählen Sie anschließend **Eigenschaften**aus.  
  
2.  Wählen Sie im Fenster **Eigenschaften** auf der rechten Seite des Bildschirms den Wert aus, der der Eigenschaft entspricht, die Sie ändern möchten, und geben Sie dann den neuen Wert ein.  
  
    > [!NOTE]  
    >  Wenn die Spaltenverwendung auf **Ignore**festgelegt wird, ist das Fenster **Eigenschaften** für die Spalte leer.  
  
     Der neue Wert wird wirksam, wenn Sie ein anderes Element im Designer auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und -anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
