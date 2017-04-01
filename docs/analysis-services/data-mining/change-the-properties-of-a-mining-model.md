---
title: "&#196;ndern der Eigenschaften eines Miningmodells | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Miningmodelle [Analysis Services], Eigenschaften"
  - "Eigenschaften [Data Mining]"
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# &#196;ndern der Eigenschaften eines Miningmodells
  Einige Miningmodelleigenschaften gelten für das gesamte Modell, wohingegen andere Modelleigenschaften für einzelne Spalten gelten. Beispiele von Eigenschaften, die für das gesamte Modell gelten, sind die **Drillthrough** -Eigenschaft, die angibt, ob die Falldaten für Abfragen verfügbar sein sollen, und die **Description** -Eigenschaft. Eigenschaften, die für die Spalte gültig sind, schließen **Usage** und **ModelingFlags**ein, die steuern, wie Daten in der Spalte im Modell verwendet werden.  
  
 Die folgenden Modelleigenschaften besitzen erweiterte Editor-Programme, mit denen Ausdrücke erstellt oder komplexe Modelleigenschaften konfiguriert werden können. Funktionen der folgenden Eigenschaften:  
  
-   **Filter**-Eigenschaft: Öffnet das [Dialogfeld „Datasetfilter oder Modellfilter“](../Topic/Data%20Set%20Filter%20or%20Model%20Filter%20Dialog%20Box.md).  
  
-   **AlgorithmParameters**-Eigenschaft: Öffnet das [Dialogfeld „Algorithmusparameter“ &#40;Miningmodelle-Sicht&#41;](../Topic/Algorithm%20Parameters%20Dialog%20Box%20\(Mining%20Models%20View\).md).  
  
 Informationen zum Festlegen der Eigenschaften eines Miningmodells finden Sie unter [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md).  
  
### So ändern Sie die Eigenschaften eines Miningmodells  
  
1.  Klicken Sie im Data Mining-Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste entweder auf den Spaltenheader, der den Namen des Miningmodells enthält, oder auf die Zeile des Rasters mit dem Namen des Miningalgorithmus. Wählen Sie anschließend **Eigenschaften** aus.  
  
2.  Wählen Sie im Fenster **Eigenschaften** auf der rechten Seite des Bildschirms den Wert aus, der der Eigenschaft entspricht, die Sie ändern möchten, und geben Sie dann den neuen Wert ein.  
  
     Der neue Wert wird wirksam, wenn Sie ein anderes Element im Designer auswählen.  
  
### So ändern Sie die Eigenschaften einer Miningmodellspalte  
  
1.  Klicken Sie im Data Mining-Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste auf die Zelle des Rasters im Schnittpunkt zwischen Miningstrukturspalte und Miningmodell. Wählen Sie anschließend **Eigenschaften** aus.  
  
2.  Wählen Sie im Fenster **Eigenschaften** auf der rechten Seite des Bildschirms den Wert aus, der der Eigenschaft entspricht, die Sie ändern möchten, und geben Sie dann den neuen Wert ein.  
  
    > [!NOTE]  
    >  Wenn die Spaltenverwendung auf **Ignore** festgelegt wird, ist das Fenster **Eigenschaften** für die Spalte leer.  
  
     Der neue Wert wird wirksam, wenn Sie ein anderes Element im Designer auswählen.  
  
## Siehe auch  
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  