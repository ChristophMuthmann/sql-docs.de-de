---
title: "Wählen Sie aus, und ordnen Sie Eingabedaten für eine Vorhersageabfrage | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tables [Analysis Services], prediction queries
- Mining Model Prediction [Analysis Services], input tables
ms.assetid: 00d330a0-879d-4da0-9f29-53c288116f4d
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b95fd2fc60fa252e8ad9de34768c12846a45e322
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="choose-and-map-input-data-for-a-prediction-query"></a>Auswählen und Zuordnen von Eingabedaten für eine Vorhersageabfrage
  Wenn Prognosen aus einem Miningmodell erstellt werden, werden im Allgemeinen neue Daten in das Modell eingegeben. (Eine Ausnahme bilden Zeitreihenmodelle, die nur Prognosen auf Grundlage von historischen Daten treffen können.) Um neue Daten für das Modell bereitstellen zu können, müssen die Daten als Teil einer Datenquellensicht verfügbar sein. Wenn Sie im Voraus wissen, welche Daten Sie für die Prognose verwenden möchten, können Sie sie in die Datenquellensicht einschließen, mit denen Sie das Modell erstellt haben. Andernfalls müssen Sie ggf. eine neue Datenquellensicht erstellen. Weitere Informationen finden Sie unter [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Gelegentlich sind die benötigten Daten möglicherweise in mehr als einer Tabelle in einem 1:n-Join enthalten. Dies trifft auf Daten zu, die für Zuordnungsmodelle oder Sequenzclustermodelle verwendet werden, für die wiederum eine Falltabelle verwendet wird, die mit einer geschachtelten Tabelle verknüpft ist, die Produkt- oder Transaktionsdetails enthält. Wenn das Modell eine für Fälle geschachtelte Tabellenstruktur verwendet, müssen die Daten, die für die Prognose verwendet werden, auch eine für Fälle geschachtelte Tabellenstruktur besitzen.  
  
> [!WARNING]  
>  Sie können keine neuen Spalten hinzufügen oder zuordnen, die sich in einer anderen Datenquellensicht befinden. Die ausgewählte Datenquellensicht muss alle Spalten enthalten, die Sie für die Vorhersageabfrage benötigen.  
  
 Nachdem Sie die Tabellen ermittelt haben, die die Daten für die Prognose enthalten, müssen Sie die Spalten in den externen Daten den Spalten im Miningmodell zuordnen. Wenn im Modell zum Beispiel eine Prognose des Kaufverhaltens von Kunden auf Grundlage demografischer Daten und Umfrageantworten dargestellt wird, sollten die Eingabedaten Informationen enthalten, die im Allgemeinen dem Inhalt des Modells entsprechen. Sie benötigen nicht für jede einzelne Spalte übereinstimmende Daten, doch eine möglichst große Zahl von Spalten mit übereinstimmenden Daten ist von Vorteil. Wenn Sie Spalten zuordnen möchten, die andere Datentypen enthalten, erhalten Sie möglicherweise einen Fehler. In diesem Fall können Sie eine benannte Berechnung in der Datenquellensicht definieren, um die neuen Spaltendaten in den Datentyp umzuwandeln bzw. zu konvertieren, der für das Modell erforderlich ist. Weitere Informationen finden Sie unter [Definieren von benannten Berechnungen in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 Wenn Sie die Daten auswählen, die Sie für die Prognose verwenden möchten, werden einige Spalten in der ausgewählten Datenquelle möglicherweise automatisch den Miningmodellspalten zugeordnet. Dies geschieht auf Grundlage der Namensähnlichkeit und der übereinstimmenden Datentypen. Sie können im Dialogfeld **Zuordnung ändern** in der **Miningmodellvorhersage** die zugeordneten Spalten ändern, fehlerhafte Zuordnungen löschen oder neue Zuordnungen für vorhandene Spalten erstellen. Die Entwurfsoberfläche **Miningmodellvorhersage** unterstützt auch die Drag &amp; Drop-Bearbeitung von Verbindungen.  
  
-   Wählen Sie eine Spalte in der Tabelle **Miningmodell** aus, und ziehen Sie sie in der Tabelle **Eingabetabelle(n) auswählen** in die entsprechende Spalte, um eine neue Verbindung zu erstellen.  
  
-   Zum Entfernen einer Verbindung wählen Sie die Verbindungslinie, und drücken Sie die ENTF-TASTE.  
  
 Die folgende Prozedur beschreibt, wie Sie im Dialogfeld **Geschachtelten Join angeben** die Joins ändern können, die zwischen der Falltabelle und einer geschachtelten Tabelle erstellt wurden, die wiederum als Eingaben für Vorhersageabfragen verwendet werden.  
  
### <a name="select-an-input-table"></a>Auswählen einer Eingabetabelle  
  
1.  Klicken Sie in der Tabelle **Eingabetabelle(n) auswählen** der Registerkarte **Mininggenauigkeitsdiagramm** im Data Mining-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Falltabelle auswählen**.  
  
     Das **Tabelle auswählen** -Dialogfeld wird geöffnet. In diesem Dialogfeld können Sie die Tabelle auswählen, die die Daten enthält, auf denen Ihre Abfragen basieren sollen.  
  
2.  Wählen Sie im Dialogfeld **Tabelle auswählen** in der Liste **Datenquelle** eine Datenquelle aus.  
  
3.  Wählen Sie unter **Tabellen-/Sichtname**die Tabelle aus, die die Daten enthält, die Sie zum Testen der Modelle verwenden möchten.  
  
4.  Klicken Sie auf **OK**.  
  
     Die Spalten der Miningstruktur werden automatisch den gleichnamigen Spalten der Eingabetabelle zugeordnet.  
  
### <a name="change-the-way-that-input-data-is-mapped-to-the-model"></a>Ändern der Methode für die Zuordnung von Eingabedaten zum Modell  
  
1.  Klicken Sie im Data Mining-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf die Registerkarte **Miningmodellvorhersage** .  
  
2.  Klicken Sie im Menü **Miningmodell** auf **Verbindungen ändern**.  
  
     Das Dialogfeld **Zuordnung bearbeiten** wird geöffnet. In diesem Dialogfeld werden in der Spalte **Miningmodellspalte** die Spalten in der ausgewählten Miningstruktur aufgeführt. In der Spalte **Tabellenspalte** werden die Spalten in der externen Datenquelle aufgeführt, die Sie im Dialogfeld **Eingabetabelle(n) auswählen** ausgewählt haben. Die Spalten in der externen Datenquelle werden den Spalten im Miningmodell zugeordnet.  
  
3.  Wählen Sie unter **Tabellenspalte**die Zeile aus, die der Miningmodellspalte entspricht, für die die Zuordnung erfolgen soll.  
  
4.  Wählen Sie eine neue Spalte in der Liste der verfügbaren Spalten in der externen Datenquelle aus. Wählen Sie das leere Element in der Liste aus, um die Spaltenzuordnung zu löschen.  
  
5.  Klicken Sie auf **OK**.  
  
     Die neuen Spaltenzuordnungen werden im Designer angezeigt.  
  
### <a name="remove-a-relationship-between-input-tables"></a>Entfernen einer Beziehung zwischen Eingabetabellen  
  
1.  Klicken Sie in der Tabelle **Eingabetabelle(n) auswählen** der Registerkarte **Miningmodellvorhersage** im Data Mining-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Join ändern**.  
  
     Das Dialogfeld **Geschachtelten Join angeben** wird geöffnet.  
  
2.  Wählen Sie eine Beziehung aus.  
  
3.  Klicken Sie auf **Beziehung entfernen**.  
  
4.  Klicken Sie auf **OK**.  
  
     Die Beziehung zwischen der Falltabelle und der geschachtelten Tabelle wird entfernt.  
  
### <a name="create-a-new-relationship-between-input-tables"></a>Erstellen einer neuen Beziehung zwischen Eingabetabellen  
  
1.  Klicken Sie in der Tabelle **Eingabetabelle(n) auswählen** der Registerkarte **Miningmodellvorhersage** im Data Mining-Designer auf **Join ändern**.  
  
     Das Dialogfeld **Geschachtelten Join angeben** wird geöffnet.  
  
2.  Klicken Sie auf **Beziehung hinzufügen**.  
  
     Das Dialogfeld **Beziehung erstellen** wird geöffnet.  
  
3.  Wählen Sie in **Quellspalten**den Schlüssel der geschachtelten Tabelle aus.  
  
4.  Wählen Sie in **Zielspalten**den Schlüssel der Falltabelle aus.  
  
5.  Klicken Sie im Dialogfeld **Beziehung erstellen** auf **OK** .  
  
6.  Klicken Sie im Dialogfeld **Geschachtelten Join angeben** auf **OK** .  
  
     Zwischen der Falltabelle und der geschachtelten Tabelle wird eine neue Beziehung erstellt.  
  
### <a name="add-a-nested-table-to-the-input-tables-of-a-prediction-query"></a>Hinzufügen einer geschachtelten Tabelle zu den Eingabetabellen einer Vorhersageabfrage  
  
1.  Klicken Sie auf der Registerkarte **Miningmodellvorhersage** im Data Mining-Designer auf **Falltabelle auswählen** , um das Dialogfeld **Tabelle auswählen** zu öffnen.  
  
    > [!NOTE]  
    >  Sie können den Eingaben keine geschachtelte Tabelle hinzufügen, sofern Sie keine Falltabelle angegeben haben. Die Verwendung einer geschachtelten Tabelle erfordert, dass in dem Miningmodell, das Sie für Vorhersagen verwenden, ebenfalls eine geschachtelte Tabelle verwendet wird.  
  
2.  Wählen Sie im Dialogfeld **Tabelle auswählen** in der Liste **Datenquelle** eine Datenquelle aus, und wählen Sie in der Datenquellensicht dann die Tabelle aus, die die Falldaten enthält. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Klicken Sie auf **Geschachtelte Tabelle auswählen** , um das Dialogfeld **Tabelle auswählen** zu öffnen.  
  
4.  Wählen Sie im Dialogfeld **Tabelle auswählen** in der Liste **Datenquelle** eine Datenquelle aus, und wählen Sie in der Datenquellensicht dann die Tabelle aus, welche die geschachtelten Daten enthält. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Falls bereits eine Beziehung besteht, werden die Spalten des Miningmodells automatisch den gleichnamigen Spalten der Eingabetabelle zugeordnet. Die Beziehung zwischen der geschachtelten Tabelle und der Falltabelle können Sie ändern, indem Sie auf **Join ändern**klicken und damit das Dialogfeld **Beziehung erstellen** öffnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Vorhersageabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  

