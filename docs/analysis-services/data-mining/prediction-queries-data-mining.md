---
title: Vorhersageabfragen (Datamining) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 55dd3cf7af1721a958ebebb70d864a1fd0b873c6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="prediction-queries-data-mining"></a>Vorhersageabfragen (Data Mining)
  Das Ziel eines typischen Data Mining-Projekts besteht darin, mithilfe des Miningmodells Vorhersagen zu treffen. Beispiel: Sie möchten die zu erwartenden Ausfallzeiten für einen bestimmten Servercluster vorhersagen oder die Wahrscheinlichkeit ermitteln, mit der bestimmte Kundensegmente auf eine Werbekampagne reagieren. Für all diese Aufgaben können Sie eine Vorhersageabfrage erstellen.  
  
 Funktionell gibt es unterschiedliche Typen von Vorhersageabfragen, die in SQL Server unterstützt wurden, abhängig von der Art der Eingabe für die Abfrage:  
  
|Abfragetyp|Abfrageoptionen|  
|----------------|-------------------|  
|SINGLETON-Vorhersageabfragen|Verwenden Sie eine SINGLETON-Abfrage, wenn Sie die Ergebnisse für einen einzelnen neuen Fall oder für mehrere neue Fälle vorhersagen möchten. Sie stellen die Eingabewerte direkt in der Abfrage bereit, und die Abfrage wird als einzelne Sitzung ausgeführt.|  
|Batchvorhersagen|Verwenden Sie Batchvorhersagen, wenn externe Daten vorliegen, die Sie an das Modell übergeben möchten und die als Grundlage für Vorhersagen dienen sollen. Um Vorhersagen für einen ganzen Satz von Daten zu treffen, ordnen Sie die Daten in der externen Quelle den Spalten im Modell zu, und geben Sie anschließend den Typ der Vorhersagedaten an, die Sie ausgeben möchten.<br /><br /> Die Abfrage für das ganze Dataset wird in einer einzelnen Sitzung ausgeführt. Diese Option ist viel effizienter als das wiederholte Senden mehrerer Abfragen.|  
|Zeitreihenvorhersagen|Verwenden Sie eine Zeitreihenabfrage, wenn Sie eine Vorhersage eines Werts für mehrere zukünftige Schritte erstellen möchten. SQL Server Data Mining stellt für Zeitreihenabfragen zusätzlich die folgende Funktionalität bereit:<br /><br /> Sie können ein vorhandenes Modell erweitern, indem Sie neue Daten als Teil der Abfrage hinzufügen, und anschließend Vorhersagen auf Grundlage der zusammengesetzten Reihe treffen.<br /><br /> Sie können ein vorhandenes Modell mit der REPLACE_MODEL_CASES-Option auf eine neue Datenreihe anwenden.<br /><br /> Sie können Kreuzvorhersagen durchführen.|  
  
 In den folgenden Abschnitten werden die allgemeine Syntax von Vorhersageabfragen und die verschiedenen Typen von Vorhersageabfragen beschrieben. Außerdem wird erläutert, wie Sie mit den Ergebnissen von Vorhersageabfragen arbeiten.  
  
 [Grundentwurf von Vorhersageabfragen](#bkmk_PredQuery)  
  
-   [Hinzufügen von Vorhersagefunktionen](#bkmk_PredFunc)  
  
-   [SINGLETON-Abfragen](#bkmk_SingletonQuery)  
  
-   [Batchvorhersageabfragen](#bkmk_BatchQuery)  
  
-   [Zeitreihenabfragen](#bkmk_TSQuery)  
  
 [Arbeiten mit den Abfrageergebnissen](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a> Grundentwurf von Vorhersageabfragen  
 Wenn Sie eine Vorhersage erstellen, geben Sie in der Regel neue Daten an und lassen das Modell auf Basis dieser neuen Daten eine Vorhersage erstellen.  
  
-   Bei einer Batchvorhersageabfrage ordnen Sie das Modell mit einem *PREDICTION JOIN*einer externen Datenquelle zu.  
  
-   In einer Singleton-Vorhersageabfrage geben Sie einen oder mehrere Werte ein, die als Eingaben verwendet werden sollen. Sie können mit einer Singleton-Vorhersageabfrage mehrere Vorhersagen erstellen. Wenn Sie jedoch viele Vorhersagen erstellen müssen, erzielen Sie mit einer Batchabfrage eine höhere Leistung.  
  
 Sowohl SINGLETON- als auch Batchvorhersageabfragen verwenden die PREDICTION JOIN-Syntax, um die neuen Daten zu definieren. Der Unterschied besteht darin, wie die Eingabeseite des PREDICTION JOINS angegeben wird.  
  
-   In einer Batchvorhersageabfrage stammen die Daten aus einer externen Datenquelle, die mit der OPENQUERY-Syntax angegeben wird.  
  
-   In einer SINGLETON-Vorhersageabfrage werden die Daten inline als Teil der Abfrage angegeben.  
  
 Bei Zeitreihenmodellen sind nicht immer Eingabedaten erforderlich. Es ist auch möglich, Vorhersagen ausschließlich anhand der bereits im Modell enthaltenen Daten zu generieren. Wenn Sie jedoch neue Eingabedaten angeben, müssen Sie entscheiden, ob Sie die neuen Daten zum Aktualisieren und Erweitern des Modells verwenden möchten, oder ob die Daten die ursprüngliche Datenreihe im Modell ersetzen sollen.  Weitere Informationen zu diesen Optionen finden Sie unter [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md).  
  
###  <a name="bkmk_PredFunc"></a> Hinzufügen von Vorhersagefunktionen  
 Sie können nicht nur einen Wert vorhersagen, sondern eine Vorhersageabfrage anpassen, um verschiedene Arten von Informationen, die mit der Vorhersage verknüpft sind, zurückzugeben. Wenn durch die Vorhersage z. B. eine Liste mit Produktempfehlungen für einen Kunden erstellt wird, können Sie auch die Wahrscheinlichkeit für jede Vorhersage ermitteln, eine Rangfolge erstellen und dem Benutzer nur die besten Empfehlungen präsentieren.  
  
 Dazu müssen Sie der Abfrage *Vorhersagefunktionen* hinzufügen. Jedes Modell oder jeder Abfragetyp unterstützt bestimmte Funktionen. Clustermodelle unterstützen beispielsweise spezielle Vorhersagefunktionen, die zusätzliche Details über die vom Modell vorgenommenen Cluster bereitstellen, wohingegen Zeitreihenmodelle über Funktionen zur Berechnung der Unterschiede im zeitlichen Verlauf verfügen. Es gibt auch allgemeine Vorhersagefunktionen, die mit fast allen Modelltypen funktionieren. Eine Liste der Vorhersagefunktionen, die in verschiedenen Abfragen unterstützt werden, finden Sie unter folgendem Thema in der DMX-Referenz: [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md).  
  
###  <a name="bkmk_SingletonQuery"></a> Erstellen von SINGLETON-Vorhersageabfragen  
 Eine SINGLETON-Vorhersageabfrage ist nützlich, wenn Sie schnelle Vorhersagen in Echtzeit erstellen möchten. Ein häufiges Szenario sind z. B. Informationen vom Kunden, die etwa über ein Formular auf einer Website abgerufen wurden und als Eingabedaten für eine SINGLETON-Vorhersageabfrage verwendet werden. Wenn ein Kunde z. B. ein Produkt aus einer Liste auswählt, können Sie diese Auswahl als Eingabe für eine Abfrage verwenden, die eine Liste geeigneter Produktempfehlungen erstellt.  
  
 SINGLETON-Vorhersageabfragen erfordern keine separate Tabelle mit Eingaben. Sie stellen stattdessen eine oder mehrere Zeilen mit Werten als Eingabe für das Modell bereit, und die Vorhersagen werden in Echtzeit zurückgegeben.  
  
> [!WARNING]  
>  Ungeachtet des Namens können SINGLETON-Vorhersageabfragen nicht nur für einzelne Vorhersagen verwendet werden – Sie können mehrere Vorhersagen für jeden Satz von Eingaben generieren. Mehrere Eingabefälle geben Sie mithilfe von SELECT-Anweisungen für jeden Eingabefall an, die Sie dann mit dem UNION-Operator kombinieren.  
  
 Beim Erstellen einer SINGLETON-Vorhersageabfrage müssen Sie die neuen Daten in Form einer PREDICTION JOIN-Anweisung für das Modell bereitstellen. Dies bedeutet, dass Sie zwar keine Zuordnung zu einer tatsächlichen Tabelle vornehmen, jedoch dennoch sicherstellen müssen, dass die neuen Daten mit den vorhandenen Spalten des Miningmodells übereinstimmen. Wenn die neuen Datenspalten und die neuen Daten genau übereinstimmen, übernimmt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Zuordnung der Spalten. Dies wird als *NATURAL PREDICTION JOIN*bezeichnet. Wenn die Spalten jedoch nicht übereinstimmen oder die neuen Daten nicht dieselbe Art und Menge von Daten enthalten wie das Modell, müssen Sie angeben, welche Spalten im Modell den neuen Daten zuzuordnen sind, oder Sie legen die fehlenden Werte fest.  
  
###  <a name="bkmk_BatchQuery"></a> Batchvorhersageabfragen  
 Eine Batchvorhersageabfrage ist nützlich, wenn Sie externe Daten vorliegen haben, die Sie für Vorhersagen verwenden möchten. Angenommen, Sie haben ein Modell erstellt, das Kunden anhand ihrer Onlineaktivität und Kaufhistorie kategorisiert. Sie können dieses Modell auf eine Liste neu abgerufener Werte anwenden, um Projektionen für Verkäufe zu erstellen oder Ziele für vorgeschlagene Kampagnen zu identifizieren.  
  
 Wenn Sie einen PREDICTION JOIN ausführen, müssen Sie die Spalten im Modell den Spalten in der neuen Datenquelle zuordnen. Daher muss die Datenquelle, die Sie für die Eingabe auswählen, Daten enthalten, die denen im Modell zumindest ähneln. Die neuen Informationen müssen nicht exakt übereinstimmen und dürfen unvollständig sein. Beispiel: Angenommen, das Modell wurde mit Informationen zu Einkommen und Alter trainiert, doch die Kundenliste, die Sie für Vorhersagen verwenden, enthält nur Angaben zum Alter und nicht zum Einkommen. In diesem Szenario können die neuen Daten immer noch dem Modell zugeordnet werden, und es kann eine Vorhersage für jeden Kunden erstellt werden. Wenn das Einkommen jedoch ein wichtiger Vorhersagefaktor für das Modell sein sollte, würde das Fehlen vollständiger Informationen die Qualität der Vorhersagen beeinflussen.  
  
 Die besten Ergebnisse erzielen Sie, wenn Sie möglichst viele der zwischen den neuen Daten und dem Modell übereinstimmenden Spalten verknüpfen. Die Abfrage wird jedoch auch dann erfolgreich durchgeführt, wenn keine Übereinstimmungen vorhanden sind. Wenn keine Spalten verknüpft werden, gibt die Abfrage die marginale Vorhersage zurück. Diese entspricht der Anweisung `SELECT <predictable-column> FROM <model>` ohne PREDICTION JOIN-Klausel.  
  
 Nachdem Sie alle relevanten Spalten erfolgreich zugeordnet haben, führen Sie die Abfrage aus. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt für jede Zeile in den neuen Daten Vorhersagen auf Grundlage der Muster im Modell. Sie können die Ergebnisse in einer neuen Tabelle in der Datenquellensicht speichern, die die externen Daten enthält, oder Sie können die Daten kopieren und einfügen, wenn Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verwenden.  
  
> [!WARNING]  
>  Wenn Sie den Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verwenden, muss die externe Datenquelle zuerst als Datenquellensicht definiert werden.  
  
 Wenn Sie einen PREDICTION JOIN mit DMX erstellen, können Sie die externe Datenquelle anhand der Befehle OPENQUERY, OPENROWSET oder SHAPE angeben. Die Standard-Datenzugriffsmethode in den DMX-Vorlagen ist OPENQUERY. Informationen zu diesen Methoden finden Sie unter [Quelldatenabfrage &#60;source data query&#62;](../../dmx/source-data-query.md).  
  
###  <a name="bkmk_TSQuery"></a> Vorhersagen für Zeitreihenminingmodelle  
 Zeitreihenmodelle unterscheiden sich von anderen Modelltypen. Sie können entweder das unveränderte Modell verwenden, um Vorhersagen zu treffen, oder Sie können neue Daten für das Modell bereitstellen, um das Modell zu aktualisieren und Vorhersagen auf Grundlage der aktuellen Trends zu erstellen. Wenn Sie neue Daten hinzufügen, können Sie angeben, wie die neuen Daten verwendet werden sollen.  
  
-   Beim*Erweitern der Modellfälle* werden die neuen Daten der vorhandenen Datenreihe im Zeitreihenmodell hinzugefügt. Damit basieren alle nachfolgenden Vorhersagen auf der neuen, kombinierten Reihe. Diese Option empfiehlt sich, wenn Sie einem vorhandenen Modell lediglich einige Datenpunkte hinzufügen möchten.  
  
     Angenommen, es ist ein Zeitreihenmodell vorhanden, das mit Umsatzdaten vom vergangenen Jahr trainiert wurde. Nachdem Sie einige Monate neue Umsatzdaten gesammelt haben, möchten Sie Ihre Verkaufsprognosen für das laufende Jahr aktualisieren. Sie können einen PREDICTION JOIN erstellen, der das Modell durch Hinzufügen neuer Daten aktualisiert und es um neue Vorhersagen erweitert.  
  
-   Beim*Ersetzen der Modellfälle* behalten Sie das trainierte Modell bei, ersetzen jedoch die zugrunde liegenden Fälle durch einen Satz neuer Falldaten. Diese Option ist nützlich, wenn Sie den Trend im Modell behalten, diesen aber auf einen anderen Satz von Daten anwenden möchten.  
  
     Das ursprüngliche Modell könnte z. B. mit einem Satz von Daten mit sehr hohen Verkaufsvolumen trainiert worden sein. Wenn Sie die zugrunde liegenden Daten durch eine neue Reihe (vielleicht aus einer Filiale mit niedrigerem Verkaufsvolumen) ersetzen, wird der Trend beibehalten, aber die Vorhersagen beginnen mit den Werten der neuen ersetzten Reihe.  
  
 Unabhängig vom verwendeten Ansatz ist der Ausgangspunkt für Vorhersagen stets das Ende der ursprünglichen Reihe.  
  
 Weitere Informationen zum Erstellen von PREDICTION JOINS für Zeitreihenmodelle finden Sie unter [Abfragebeispiel Zeitreihenmodell](../../analysis-services/data-mining/time-series-model-query-examples.md) oder [PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md).  
  
##  <a name="bkmk_WorkResults"></a> Arbeiten mit den Ergebnissen einer Vorhersageabfrage  
 Die Optionen zum Speichern der Ergebnisse einer Data Mining-Vorhersageabfrage unterscheiden sich abhängig von der Methode der Abfragenerstellung.  
  
-   Wenn Sie mit dem Vorhersage-Abfrage-Generator entweder in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]eine Abfrage erstellen, können Sie die Ergebnisse einer Vorhersageabfrage in einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle speichern. Weitere Informationen finden Sie unter [Anzeigen und Speichern der Ergebnisse einer Vorhersageabfrage](../../analysis-services/data-mining/view-and-save-the-results-of-a-prediction-query.md).  
  
-   Wenn Sie Vorhersageabfragen mit DMX im Abfragebereich von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen, können Sie mithilfe der Abfrageausgabemöglichkeiten die Ergebnisse in einer Datei oder im Bereich der Abfrageergebnisse als Text oder in einem Raster speichern. Weitere Informationen finden Sie unter [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
-   Wenn Sie mit den Integration Services-Komponenten eine Vorhersageabfrage ausführen, bieten die Tasks die Möglichkeit, die Ergebnisse mithilfe eines verfügbaren ADO.NET- oder OLEDB-Verbindungs-Managers in eine Datenbank zu schreiben. Weitere Informationen finden Sie unter [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
 Sie müssen sich darüber im Klaren sein, dass die Ergebnisse einer Vorhersageabfrage nicht den Ergebnissen einer Abfrage in einer relationalen Datenbank entsprechen, die immer eine einzelne Zeile mit verknüpften Werten zurückgibt. Jede DMX-Vorhersagefunktion, die Sie einer Abfrage hinzufügen, gibt ein eigenes Rowset zurück. Wenn Sie eine Vorhersage für einen Einzelfall treffen, kann das Ergebnis aus einem vorhergesagten Wert und mehreren Spalten geschachtelter Tabellen mit zusätzlichen Details bestehen.  
  
 Wenn Sie mehrere Funktionen in einer Abfrage kombinieren, werden die Rückgabeergebnisse als hierarchisches Rowset kombiniert. Beispiel: Sie verwenden ein Zeitreihenmodell, um zukünftige Werte für Umsatz und Verkaufsmenge vorherzusagen, und zwar mithilfe einer Abfrage wie der folgenden DMX-Anweisung:  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 Die Ergebnisse dieser Abfrage sind zwei Spalten, und zwar jeweils eine Spalte für jede vorhergesagte Reihe, wobei jede Zeile eine geschachtelte Tabelle mit den vorhergesagten Werten enthält:  
  
 **PredictedAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Amount|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|Quantity|  
|-----------|--------------|  
|201102|260|  
  
 Wenn Ihr Anbieter keine hierarchischen Rowsets verarbeiten kann, können Sie die Ergebnisse mit dem FLATTEN-Schlüsselwort in der Vorhersageabfrage vereinfachen. Weitere Informationen sowie Beispiele vereinfachter Rowsets finden Sie unter [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Inhaltsabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-queries-data-mining.md)   
 [Datendefinitionsabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/data-definition-queries-data-mining.md)  
  
  
