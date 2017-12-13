---
title: "Erstellen eine Vorhersageabfrage mithilfe des Generators für Vorhersageabfragen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- Mining Model Prediction [Analysis Services], prediction queries
ms.assetid: e02836e5-dd8c-4c97-a078-840ae79d3660
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c7d6511a36b9a59e20908feffdb0f61a907377ed
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="create-a-prediction-query-using-the-prediction-query-builder"></a>Erstellen von Vorhersageabfragen mithilfe des Generators für Vorhersageabfragen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können Vorhersageabfragen entweder beim Erstellen einer Datamining-Projektmappe in BI Development Studio oder durch Rechtsklick auf ein vorhandenes Miningmodell in SQL Server Management Studio, und wählen Sie dann die Option **Vorhersageabfrage erstellen**.  
  
 Der **Generator für Vorhersageabfragen** verfügt über die folgenden drei Entwurfsmodi, zwischen denen Sie wechseln können, indem Sie auf die Symbole in der Ecke links oben klicken.  
  
-   **Entwerfen**  
  
-   **Abfrage**  
  
-   **Ergebnis**  
  
 Mit dem**Entwurfsmodus** können Sie eine Vorhersageabfrage erstellen, indem Sie die Eingabedaten auswählen, dem Modell die Daten zuordnen und anschließend die Vorhersagefunktionen den Anweisungen hinzufügen, die Sie durch die Verwendung des Rasters erstellt haben. Der Entwurfsbereich enthält diese Bausteine:  
  
 **Quelle**  
 Wählen Sie die Quelle der neuen Spalte aus. Sie können Spalten aus dem Miningmodell, in der Datenquellenansicht enthaltene Eingabetabellen, eine Vorhersagefunktion oder einen benutzerdefinierten Ausdruck verwenden.  
  
 **Feld**  
 Bestimmt die spezielle Spalte oder Funktion, die mit der Auswahl in der Spalte **Quelle** verbunden ist.  
  
 **Alias**  
 Bestimmt, wie die Spalte im Resultset benannt wird.  
  
 **Anzeigen**  
 Bestimmt, ob die Auswahl in der Spalte **Quelle** in den Ergebnissen angezeigt wird.  
  
 **Gruppieren**  
 Verwendet die Spalte **Und/Oder** , um Ausdrücke mithilfe von Klammern zu gruppieren. Beispielsweise (expr1 oder expr2) und expr3.  
  
 **Und/Oder**  
 Erstellt einen logischen Ausdruck in der Abfrage. Beispielsweise (expr1 oder expr2) und expr3.  
  
 **Kriterium/Argument**  
 Gibt eine Bedingung oder einen benutzerdefinierten Ausdruck an, der auf die Spalte angewendet wird. Sie können Spalten aus den Tabelle in die Zelle ziehen.  
  
 Im**Abfragemodus** steht ein Text-Editor bereit, mit dem Sie direkt auf die Data Mining-Erweiterungssprache (DMX) zugreifen können, und mit dem Sie Eingabedaten und Modellspalten anzeigen können. Wenn Sie den **Abfragemodus** auswählen, wird das Raster, mit dessen Hilfe Sie die Abfrage definiert haben, durch einen einfachen Texteditor ersetzt. Sie können diesen Editor verwenden, um von Ihnen erstellte Abfragen zu kopieren und zu speichern oder um sie in vorhandene DMX-Abfragen aus der Zwischenablage einzufügen und sie auszuführen.  
  
 In der**Ergebnissicht** werden die aktuelle Abfrage ausgeführt und die Ergebnisse in einem Raster angezeigt. Wenn sich die zugrunde liegenden Daten geändert haben und Sie die Abfrage erneut ausführen möchten, klicken Sie auf der Statusleiste auf die Schaltfläche zum Abspielen.  
  
 Sie können eine Data Mining-Abfrage entwerfen, indem Sie die visuellen Tools und den Texteditor zusammen verwenden. Wenn Sie im Texteditor Änderungen an der Abfrage vornehmen und zurück zur **Entwurfsansicht** wechseln, gehen alle Änderungen verloren. Die Abfragen werden dann zur ursprünglichen Abfrage zurückgesetzt, die mit dem Generator für Vorhersageabfragen erstellt wurde.  
  
### <a name="to-create-a-prediction-query"></a>So erstellen Sie eine Vorhersageabfrage  
  
1.  Klicken Sie auf die **Miningmodellvorhersage** -Registerkarte im Data Mining-Designer.  
  
2.  Klicken Sie in der **Miningmodell** -Tabelle auf **Modell auswählen** .  
  
     Das Dialogfeld **Miningmodell auswählen** wird geöffnet. Es zeigt alle Miningstrukturen an, die im aktuellen Projekt vorhanden sind.  
  
3.  Wählen Sie das Modell aus, für das Sie eine Vorhersage erstellen möchten, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie in der **Eingabetabelle(n) auswählen** -Tabelle auf **Falltabelle auswählen**.  
  
     Das Dialogfeld **Tabelle auswählen** wird geöffnet.  
  
5.  Wählen Sie in der Liste **Datenquelle** die Datenquelle aus, die die Daten enthält, mit denen eine Vorhersage erstellt werden soll.  
  
6.  Wählen Sie im Feld **Tabellen-/Sichtname** die Tabelle aus, die die Daten enthält, mit denen eine Vorhersage erstellt werden soll, und klicken Sie dann auf **OK**.  
  
     Wenn Sie die Eingabetabelle ausgewählt haben, erstellt der Generator für Vorhersageabfragen eine Standardzuordnung zwischen dem Miningmodell und der Eingabetabelle, die auf den Spaltennamen basiert. Um eine Zuordnung zu löschen, markieren Sie die Linie, die die Spalte der Tabelle **Miningmodell** mit der Spalte der Tabelle **Eingabetabelle(n) auswählen** verbindet, und drücken Sie dann ENTF. Sie können Zuordnungen auch manuell erstellen, indem Sie in der **Eingabetabelle(n) auswählen** -Tabelle auf eine Spalte klicken und diese dann in die **Miningmodell** -Tabelle auf die entsprechende Spalte ziehen.  
  
7.  Fügen Sie dem Raster des Generators für Vorhersageabfragen eine beliebige Kombination der folgenden drei Arten von Informationen hinzu:  
  
    -   Vorhersagbare Spalten aus dem Feld **Miningmodell** .  
  
    -   Eine beliebige Kombination aus Eingabespalten aus dem Feld **Eingabetabelle(n) auswählen** .  
  
    -   Vorhersagefunktionen  
  
8.  Führen Sie die Abfrage aus, indem Sie auf der Symbolleiste der Registerkarte **Miningmodellvorhersage** auf die erste Schaltfläche klicken und dann **Ergebnis**auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer SINGLETON-Abfrage im Data Mining-Designer](../../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)   
 [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
