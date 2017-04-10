---
title: "Modell mit dem Microsoft-Viewer f&#252;r neuronale Netzwerke durchsuchen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Miningmodellinhalte, anzeigen"
  - "Klassifizierungsminingmodell [Analysis Services]"
  - "Microsoft-Viewer für neuronale Netzwerke"
  - "Regressionsalgorithmen [Analysis Services]"
  - "Viewer für neuronale Netzwerke [Analysis Services]"
  - "neuronales Netzwerkmodell [Analysis Services]"
ms.assetid: 2343d746-c4f4-499b-9d3c-17d63310a9a3
caps.latest.revision: 43
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 43
---
# Modell mit dem Microsoft-Viewer f&#252;r neuronale Netzwerke durchsuchen
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für neuronale Netzwerke in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zeigt Miningmodelle an, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus erstellt wurden. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Algorithmus für neuronale Netzwerke erstellt Klassifizierungs- und Regressionsminingmodelle, die mehrere Eingaben und Ausgaben analysieren können, und ist für unbegrenzte Analysen und Untersuchungen sehr nützlich. Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Neural Network Algorithm](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md).  
  
 Wenn Sie mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für neuronale Netzwerke ein Modell untersuchen, wählen Sie in der Regel ein Zielattribut und einen Status aus, und anschließend wird mit dem Viewer angezeigt, wie Eingabeattribute das Ergebnis beeinflussen.  
  
 Beispiel: Angenommen, Ihnen sind die folgenden Fakten über eine Klasse von potenziellen Kunden bekannt:  
  
-   Mittleren Alters (40 bis 50 Jahre alt).  
  
-   Eigenheimbesitzer.  
  
-   Hat zwei Kinder, die noch zu Hause wohnen.  
  
 Wie können Sie diese Daten mit der Wahrscheinlichkeit in Beziehung setzen, dass der Kunde einen Kauf tätigt?  
  
 Durch Erstellen eines neuronalen Netzwerkmodells unter Berücksichtigung des Kaufverhaltens als Zielergebnis können Sie mehrere Kombinationen von Kundendaten untersuchen, z. B. hohes Einkommen, und feststellen, welche Kombination von Daten die größte Wahrscheinlichkeit einer Beeinflussung des Kaufverhaltens bietet. Sie stellen zum Beispiel fest, dass der bestimmende Faktor die Entfernung zur Arbeitsstelle ist.  
  
 Wenn Sie ausführlichere Informationen benötigen, z. B. die Formeln, die jedes erkannte Muster darstellen, können Sie die Ansichten wechseln und den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer verwenden. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) oder [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md).  
  
##  <a name="BKMK_ViewerTabs"></a> Viewer-Registerkarten  
 Wenn Sie ein Miningmodell in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]durchsuchen, wird das Modell im Data Mining-Designer auf der Registerkarte **Miningmodell-Viewer** mit dem jeweils geeigneten Viewer für das Modell angezeigt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für neuronale Netzwerke stellt die folgenden Registerkarten zum Durchsuchen von Miningmodellen in neuronalen Netzwerken bereit:  
  
-   [Eingaben](#BKMK_Inputs)  
  
-   [Ausgaben](#BKMK_Outputs)  
  
-   [Variablen](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> Eingaben  
 Wählen Sie auf der Registerkarte **Eingaben** die Attribute und Werte aus, die vom Modell als Eingaben verwendet wurden. Standardmäßig wird der Viewer mit allen enthaltenen Daten bzw. Attributen geöffnet. In dieser Standardansicht wählt das Modell aus, welche Attributwerte beim Anzeigen Priorität besitzen.  
  
 Um ein Eingabeattribut auszuwählen, klicken Sie in der Spalte **Attribut** auf das Raster **Eingabe**, und wählen Sie aus der Dropdownliste ein Attribut aus. (Nur Attribute, die im Modell eingeschlossen sind, werden in die Liste aufgenommen.)  
  
 Der erste unterschiedliche Werte wird unter der Spalte **Wert** angezeigt. Durch Anklicken des Standardwerts wird eine Liste angezeigt, die alle möglichen Status des verbundenen Attributs enthält. Sie können den Status auswählen, den Sie untersuchen möchten. Sie können beliebig viele Attribute auswählen.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> Ausgaben  
 Wählen Sie auf der Registerkarte **Ausgaben** das zu überprüfende Ergebnisattribut aus. Sie können zwei beliebige Ergebnisstatuswerte auswählen, die Sie vergleichen möchten, vorausgesetzt, dass die Spalten beim Erstellen des Modells als prognostizierbare Attribute definiert wurden.  
  
 Verwenden Sie die Liste **Ausgabeattribut**, um ein Attribut auszuwählen. Sie können zwei Status auswählen, die mit dem Attribut aus den Listen **Wert 1** und **Wert 2** verknüpft sind. Diese beiden Status der Ausgabeattribute werden im Bereich **Variablen** verglichen.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Variablen  
 Das Raster auf der Registerkarte **Variablen** enthält die folgenden Spalten: **Attribut**, **Wert**, **Begünstigt [value 1]** und **Begünstigt [value 2]**. Standardmäßig werden die Spalten nach der Stärke von **Begünstigt [value 1]** sortiert. Durch Klicken auf die Spaltenkopfzeilen wird die Reihenfolge der Inhalte der ausgewählten Spalte verändert.  
  
 Ein Balken rechts neben dem Attribut zeigt an, welchen Status des Ausgabeattributs der angegebene Eingabeattributstatus bevorzugt. Die Größe des Balkens zeigt an, wie stark der Ausgabestatus den Eingabestatus bevorzugt.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
## Siehe auch  
 [Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Tasks und Anweisungen für Miningmodell-Viewer](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Tasks und Anweisungen für Miningmodell-Viewer](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Data Mining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Data Mining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  