---
title: "Ausw&#228;hlen und Zuordnen von Modelltestdaten | Microsoft Docs"
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
  - "Spalten, [Data Mining], Genauigkeitsdiagramme für Mining"
  - "Genauigkeitsdiagramm für Mining [Analysis Services], Spaltenzuordnungen"
  - "Eingabespaltenzuordnung [Analysis Services]"
  - "Zuordnen von Eingabespalten [Analysis Services]"
ms.assetid: be0d9f20-40c3-4dac-81da-281cfe724126
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 44
---
# Ausw&#228;hlen und Zuordnen von Modelltestdaten
  Um in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ein Genauigkeitsdiagramm zu erstellen, müssen Sie die Daten auswählen, die zum Testen des Modells verwendet werden und die Daten dem Modell zuordnen.  
  
 Standardmäßig verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Miningmodelltestdaten, vorausgesetzt, dass bei der Erstellung der Miningstruktur ein zurückgehaltenes Dataset erstellt wurde. Die Erstellung eines zurückgehaltenen Testsatzes ist die einfachste Möglichkeit, Modelle zu testen, die auf der gleichen Miningstruktur basieren, da die Spaltennamen und Datentypen immer dem Modell entsprechen, und Sie können davon ausgehen, dass die Verteilung der Daten auf ähnliche Weise erfolgt. Außerdem erstellt der Designer die Beziehungen zwischen den Eingabe- und Modellspalten automatisch.  
  
 Alternativ können Sie eine externe Datenquelle angeben. Für externe Daten gelten einige zusätzliche Anforderungen:  
  
-   Das externe Dataset muss in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]als Datenquellensicht definiert werden.  
  
-   Das externe Dataset muss mindestens eine Spalte enthalten, die der vorhersagbaren Spalte im Miningmodell zugeordnet werden kann. Sie können einige Spalten ignorieren.  
  
-   Sie können keine neuen Spalten hinzufügen oder zuordnen, die sich in einer anderen Datenquellensicht befinden. Die ausgewählte Datenquellensicht muss alle Spalten enthalten, die Sie für die Vorhersageabfrage benötigen.  
  
-   Wenn die externen Spaltennamen genau den Namen im Modell entsprechen, ordnet der Designer sie für Sie zu. Wenn die Zuordnungen falsch sind, können Sie sie ändern bzw. löschen und neue Zuordnungen für vorhandene Spalten erstellen.  
  
-   Wenn Sie eine externe Datenquelle verwenden, können Sie Filter anwenden, um die Testdaten auf eine relevante Teilmenge von Fällen zu beschränken.  
  
-   Auch wenn Sie den zurückgehaltenen Testsatz verwenden, beachten Sie, dass Filter Unterschiede zwischen den Testdaten verursachen können, die einer Miningstruktur und den Miningmodelltestfällen zugeordnet sind.  
  
 In diesem Thema wird beschrieben, wie die Testdaten ausgewählt und zugeordnet werden:  
  
 [Auswählen von Eingabetabellen zum Testen der Genauigkeit eines Miningmodells](#bkmk_SelectInputs)  
  
 [Zuordnen von Modellspalten zu den Spalten in den Testdaten](#bkmk_MapColumns)  
  
 [Ändern der Methode für die Zuordnung von Spalten in den Testdaten zum Modell](#bkmk_ChangeMappings)  
  
##  <a name="bkmk_SelectInputs"></a> So wählen Sie Eingabetabellen zum Testen der Genauigkeit eines Miningmodells aus  
  
1.  Doppelklicken Sie im Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] auf die Miningstruktur, die das Modell enthält, das Sie darstellen möchten.  
  
2.  Klicken Sie auf die Registerkarte **Mininggenauigkeitsdiagramm** .  
  
3.  Wählen Sie auf der Registerkarte **Eingabeauswahl** der Sicht **Mininggenauigkeitsdiagramm** eine der folgenden Optionen aus:  
  
     **Testfälle für Miningmodell verwenden**  
  
     **Testfälle für Miningstruktur verwenden**  
  
     **Anderes Dataset verwenden**  
  
4.  Wenn Sie **Anderes Dataset verwenden**auswählen, können Sie optional auf **Filter-Editor öffnen** klicken, um Filterbedingungen für das Eingabedataset zu erstellen. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf die Registerkarte **Prognosegütediagramm** oder **Klassifikationsmatrix** , um die von Ihnen festgelegten Testdaten für die automatische Erstellung des Diagramms zu verwenden.  
  
##  <a name="bkmk_MapColumns"></a> So ordnen Sie Modellspalten den Spalten in den Testdaten zu  
  
1.  Doppelklicken Sie auf die Miningstruktur, die das Modell enthält, das Sie darstellen möchten. Daraufhin werden die Struktur und die Modelle im Data Mining-Designer geöffnet.  
  
2.  Wählen Sie die Registerkarte **Mininggenauigkeitsdiagramm** und anschließend die Registerkarte **Eingabeauswahl** aus.  
  
3.  Wählen Sie auf der Registerkarte **Eingabeauswahl** unter **Dataset auswählen, das für das Genauigkeitsdiagramm verwendet werden soll**die Option **Anderes Dataset verwenden**aus.  
  
4.  Klicken Sie auf die Schaltfläche zum Durchsuchen (**…**), um ein Dialogfeld zu öffnen und die Definition des externen Datasets zu erstellen.  
  
5.  Wählen Sie im Dialogfeld **Miningstruktur auswählen** die Miningstruktur aus, mit der Sie arbeiten wollen, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie im Data Mining-Designer in der Tabelle **Eingabetabelle(n) auswählen** der Registerkarte **Mininggenauigkeitsdiagramm** auf **Falltabelle auswählen**, um das Dialogfeld **Falltabelle auswählen** zu öffnen.  
  
7.  Wählen Sie im Dialogfeld **Tabelle auswählen** in der Liste **Datenquelle** eine Datenquelle aus. Wählen Sie die Tabelle mit den Daten aus, die Sie in den Vorhersageabfragen verwenden möchten, mit denen die Genauigkeit der Modelle ermittelt werden soll.  
  
8.  Wählen Sie im Feld **Tabellen-/Sichtname** die Tabelle aus, die die Daten enthält, die zum Testen der Modelle verwendet werden sollen.  
  
9. Bearbeiten Sie gegebenenfalls die Zuordnungen. Die Spalten der Miningstruktur werden automatisch den gleichnamigen Spalten der Eingabetabelle zugeordnet. Um Zuordnungen manuell zu erstellen, klicken Sie in der Tabelle **Eingabetabelle(n) auswählen** auf eine Spalte, und ziehen Sie diese auf die entsprechende Spalte der Tabelle **Miningstruktur**. Um eine Zuordnung zu löschen, klicken Sie auf die Linie, die die Spalte der Tabelle **Miningstruktur** mit der Spalte der Tabelle **Eingabetabelle(n) auswählen** verbindet, und drücken Sie dann ENTF.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_ChangeMappings"></a> So ändern Sie die Methode für Zuordnung von Eingabedaten zum Modell  
  
1.  Doppelklicken Sie im Data Mining-Designer auf die Struktur mit den Modellen, die Sie im Diagramm darstellen möchten.  
  
2.  Klicken Sie auf die Registerkarte **Mininggenauigkeitsdiagramm** .  
  
3.  Klicken Sie auf die Registerkarte **Eingabeauswahl** .  
  
4.  Wählen Sie unter **Dataset auswählen, das für das Genauigkeitsdiagramm verwendet werden soll**die Option **Anderes Dataset verwenden**.  
  
5.  Klicken Sie auf die Schaltfläche zum Durchsuchen (**…**), um ein Dialogfeld zu öffnen und die Definition der externen Datenquelle zu erstellen.  
  
6.  Klicken Sie im Dialogfeld **Spaltenzuordnung angeben** auf **Falltabelle auswählen**.  
  
7.  Wählen Sie im Dialogfeld Tabelle auswählen eine Datenquellensicht aus der Liste aus, und wählen Sie dann die Tabelle aus, die die Falldaten enthält. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Wenn die benötigten Tabellen nicht verfügbar sind, schließen Sie das Dialogfeld, und erstellen Sie eine neue Datenquellensicht, die die Tabelle enthält. Informationen zum Erstellen einer Datenquellensicht finden Sie unter [Definieren einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md).  
  
9. Wenn das Miningmodell eine geschachtelte Tabelle enthält, klicken Sie auf **Geschachtelte Tabelle auswählen**, und wählen Sie die geschachtelte Tabelle aus der Liste der Tabellen in der Datenquellensicht aus. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Wählen Sie die Joinlinie der Zuordnung aus, die Sie ändern möchten, und wählen Sie **Verbindungen ändern**aus.  
  
     Das Dialogfeld **Zuordnung bearbeiten** wird geöffnet. In der Tabelle in diesem Dialogfeld werden unter **Miningstrukturspalte** alle Spalten aufgeführt, die die ausgewählte Miningstruktur enthalten. Unter **Tabellenspalte** werden die Spalten aus Eingabetabellen aufgelistet, die Spalten in der Miningstruktur zugeordnet sind.  
  
11. Wählen Sie unter **Tabellenspalte**die Zeile aus, die der Zeile unter **Miningstrukturspalte** entspricht, für die Sie eine Beziehung ändern wollen. Wählen Sie eine neue Spalte in der Liste aus, oder wählen Sie den leeren Eintrag in der Liste aus, um die Spalte zu löschen.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Die neuen Spaltenzuordnungen werden im Dialogfeld **Spaltenzuordnung angeben** angezeigt. Sie können eine Zuordnung entfernen, indem Sie die Linie zwischen den Spalten auswählen und die ENTF-Taste drücken. Sie können eine neue Verbindung erstellen, indem Sie in der **Miningstruktur**-Tabelle eine Spalte auswählen und diese Spalte auf die entsprechende Spalte in der **Eingabetabelle(n) auswählen**-Tabelle ziehen.  
  
## Siehe auch  
 [Tasks und Anweisungen für Test und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  