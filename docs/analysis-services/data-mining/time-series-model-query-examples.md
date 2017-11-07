---
title: Time Series-Modell Abfragebeispiele | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b43b6b6144931dea129aeb82531fdbc5204121d0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="time-series-model-query-examples"></a>Abfragebeispiel Zeitreihenmodell
  Beim Erstellen einer Abfrage für ein Data Mining-Modell können Sie entweder eine Inhaltsabfrage oder eine Vorhersageabfrage auswählen. Die Inhaltsabfrage liefert Details über die bei der Analyse ermittelten Muster. Die Vorhersageabfrage nimmt hingegen Vorhersagen für neue Daten anhand der im Modell befindlichen Muster vor. Eine Inhaltsabfrage für ein Zeitreihenmodell bietet möglicherweise zusätzliche Angaben zu den erkannten periodischen Strukturen, wohingegen eine Vorhersageabfrage Vorhersagen für die nächsten 5 bis 10 Zeitscheiben bietet. Mit einer Abfrage können Sie auch Metadaten zum Modell abrufen.  
  
 In diesem Abschnitt wird erläutert, wie diese beiden Abfragetypen für Modelle erstellt werden, die auf dem Microsoft Time Series-Algorithmus basieren.  
  
 **Inhaltsabfragen**  
  
 [Abrufen von Periodizitätshinweisen für das Modell](#bkmk_Query1)  
  
 [Abrufen der Gleichung für ein ARIMA-Modell](#bkmk_Query2)  
  
 [Abrufen der Gleichung für ein ARTxp-Modell](#bkmk_Query3)  
  
 **Vorhersageabfragen**  
  
 [Grundlegendes zum Ersetzen und Erweitern von Zeitreihendaten](#bkmk_ReplaceExtend)  
  
 [Treffen von Vorhersagen mit EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [Treffen von Vorhersagen mit REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
 [Ersetzen von fehlenden Werten in Zeitreihenmodellen](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>Abrufen von Informationen zu einem Zeitreihenmodell  
 Eine Modellinhaltsabfrage kann grundlegende Informationen zum Modell bereitstellen. Dazu gehören beispielsweise die Parameter, die beim Erstellen des Modells verwendet wurden, und die Uhrzeit der letzten Modellverarbeitung. Das folgende Beispiel veranschaulicht die Grundsyntax für die Abfrage des Modellinhalts anhand von Data Mining-Schemarowsets.  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Abrufen von Periodizitätshinweisen für das Modell  
 Sie können die Periodizitäten abrufen, die innerhalb der Zeitreihe gefunden wurden, indem Sie eine Abfrage der ARIMA-Struktur oder der ARTXP-Struktur durchführen. Die Periodizitäten im vollständigen Modell stimmen jedoch möglicherweise nicht mit den Perioden überein, die Sie beim Erstellen des Modells als Hinweise festgelegt haben. Um die Hinweise, die beim Erstellen des Modells als Parameter bereitgestellt wurden, abzurufen, können Sie eine Abfrage für das Schemarowset des Miningmodells ausführen und dabei die folgende DMX-Anweisung verwenden:  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 Teilergebnisse:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.1,MINIMUM_SUPPORT=10,PERIODICITY_HINT={1,3},….|  
  
 Der Standardperiodizitätshinweis ist \{1\} und wird in allen Modellen angezeigt. Dieses Beispielmodell wurde mit einem zusätzlichen Hinweis erstellt, der möglicherweise nicht im endgültigen Modell vorhanden ist.  
  
> [!NOTE]  
>  Die Ergebnisse wurden für bessere Lesbarkeit hier abgeschnitten.  
  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Abrufen der Gleichung für ein ARIMA-Modell  
 Sie können die Gleichung für ein ARIMA-Modell abrufen, indem Sie eine Abfrage für einen Knoten in einer individuellen Struktur durchführen. Beachten Sie, dass jede Struktur in einem ARIMA-Modell eine andere Periodizität darstellt und dass, wenn es mehrere Datenreihen gibt, jede Datenreihe einen eigenen Satz an Periodizitätsstrukturen hat. Um die Gleichung für eine spezifische Datenreihe abzurufen, müssen Sie daher zuerst die Struktur identifizieren.  
  
 Beispielsweise sagt das TA-Präfix aus, dass der Knoten Teil einer ARIMA-Struktur ist, während das TS-Präfix auf eine ARTXP-Struktur hinweist. Eine Übersicht über die ARIMA-Stammstrukturen erhalten Sie durch Abfragen des Modellinhalts für Knoten mit dem NODE_TYPE-Wert 27. Den ARIMA-Stammknoten für eine bestimmte Datenreihe können Sie auch anhand des ATTRIBUTE_NAME-Werts ermitteln. Mit der folgenden Abfrage werden beispielsweise die ARIMA-Knoten gefunden, die die verkaufte Menge an R250-Modellen in Europa darstellen.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 Mit dieser Knoten-ID können Sie Details über die ARIMA-Formel für die Struktur abrufen. Die folgende DMX-Anweisung wird verwendet, um die Kurzform der ARIMA-Formel für die Datenreihe abzurufen. Sie ruft auch das konstante Glied aus der geschachtelten NODE_DISTRIBUTION-Tabelle ab. In diesem Beispiel wird die Formel durch Verweisen auf die eindeutige Knoten-ID TA00000007 ermittelt. Möglicherweise müssen Sie jedoch eine andere Knoten-ID verwenden, und die Ergebnisse weichen geringfügig vom Modell ab.  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 Beispielergebnisse:  
  
|Kurze Gleichung|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24….|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 Weitere Informationen zur Interpretation dieser Information finden Sie unter [Miningmodellinhalt von Zeitreihenmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Abrufen der Gleichung für ein ARTXP-Modell  
 Bei einem ARTxp-Modell werden auf jeder Ebene der Struktur andere Informationen gespeichert. Weitere Informationen zur Struktur eines ARTxp-Modells, und wie die Information in der Gleichung interpretiert werden soll, finden Sie unter [Miningmodellinhalt von Zeitreihenmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 Die folgende DMX-Anweisung ruft Teilinformationen für eine ARTxp-Struktur ab, die die verkaufte Menge an R250-Modellen in Europa darstellt.  
  
> [!NOTE]  
>  Der Name der verschachtelten Tabellenspalte VARIANCE muss in Klammern eingeschlossen werden, um ihn von dem reservierten Schlüsselwort mit dem gleichen Namen unterscheiden zu können. Die geschachtelten Tabellenspalten PROBABILITY und SUPPORT sind nicht eingeschlossen, da sie in den meisten Fällen leer sind.  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 Weitere Informationen zur Interpretation dieser Information finden Sie unter [Miningmodellinhalt von Zeitreihenmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
  
## <a name="creating-predictions-on-a-time-series-model"></a>Erstellen von Vorhersagen für ein Zeitreihenmodell  
 Ab [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]können Sie einem Zeitreihenmodell neue Daten hinzufügen und die neuen Daten automatisch in das Modell einbeziehen. Es gibt zwei Möglichkeiten, einem Zeitreihen-Miningmodell neue Daten hinzuzufügen:  
  
-   Verknüpfen Sie mit **PREDICTION JOIN** Daten in einer externen Quelle mit den Trainingsdaten.  
  
-   Bereitstellen von Daten in einzelnen Slices mit einer SINGLETON-Vorhersageabfrage Informationen zum Erstellen einer Singleton-Vorhersageabfrage finden Sie unter [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
###  <a name="bkmk_ReplaceExtend"></a> Grundlegendes zum Verhalten von Vorgängen zum Ersetzen und Erweitern  
 Wenn Sie einem Zeitreihenmodell neue Daten hinzufügen, können Sie angeben, ob die Trainingsdaten erweitert oder ersetzt werden sollen:  
  
-   **Erweitern:** Wenn Sie eine Datenreihe erweitern, werden die neuen Daten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] am Ende der vorhandenen Trainingsdaten hinzugefügt. Die Anzahl der Trainingsfälle wird ebenfalls erhöht.  
  
     Das Erweitern der Modellfälle ist sinnvoll für das kontinuierliche Aktualisieren des Modells mit neuen Daten. Wenn z. B. der Trainingssatz im Zeitverlauf zunehmen soll, können Sie einfach das Modell erweitern.  
  
     Zum Erweitern der Daten erstellen Sie einen **PREDICTION JOIN** für ein Zeitreihenmodell, geben die Quelle für die neuen Daten an und verwenden das **EXTEND_MODEL_CASES** -Argument.  
  
-   **Ersetzen:** Wenn Sie die Daten in der Datenreihe ersetzen, behält [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das trainierte Modell bei, verwendet jedoch die neuen Datenwerte zum Ersetzen einiger oder aller vorhandener Trainingsfälle. Die Größe der Trainingsdaten wird daher nicht geändert, die Fälle selbst werden jedoch kontinuierlich durch neuere Daten ersetzt. Wenn Sie genug neue Daten angeben, können Sie die Trainingsdaten durch eine vollkommen neue Reihe ersetzen.  
  
     Das Ersetzen der Modellfälle ist sinnvoll, wenn Sie ein Modell mit einem Satz von Fällen trainieren und dieses Modell auf eine andere Datenreihe anwenden möchten.  
  
     Zum Ersetzen der Daten erstellen Sie einen **PREDICTION JOIN** für ein Zeitreihenmodell, geben die Quelle für die neuen Daten an und verwenden das **REPLACE_MODEL_CASES** -Argument.  
  
> [!NOTE]  
>  Wenn Sie neue Daten hinzufügen, sind keine Vergangenheitsvorhersagen möglich.  
  
 Vorhersagen beginnen unabhängig davon, ob Sie die Trainingsdaten erweitern oder ersetzen, immer mit dem Zeitstempel am Ende des ursprünglichen Trainingssatzes. Wenn die neuen Daten also n Zeitscheiben enthalten und Sie Vorhersagen für die Zeitschritte 1 bis n anfordern, stimmen die Vorhersagen mit dem gleichen Zeitraum wie die neuen Daten überein, und Sie erhalten keine neuen Vorhersagen.  
  
 Wenn Sie neue Vorhersagen für Zeiträume benötigen, die nicht mit den neuen Daten überlappen, müssen die Vorhersagen entweder bei Zeitscheibe n+1 starten, oder Sie müssen sicherstellen, dass Sie zusätzliche Zeitscheiben anfordern.  
  
 Nehmen Sie z. B. an, dass das vorhandene Modell Daten zu sechs Monaten umfasst. Sie möchten dieses Modell erweitern, indem Sie die Umsatzdaten der letzten drei Monate hinzufügen. Gleichzeitig möchten Sie eine Vorhersage für die nächsten drei Monate treffen. Damit beim Hinzufügen von neuen Daten nur die neuen Vorhersagen abgerufen werden, geben Sie als Startpunkt Zeitscheibe 4 und als Endpunkt Zeitscheibe 7 an. Sie könnten auch insgesamt sechs Vorhersagen anfordern, die Zeitscheiben für die ersten drei Vorhersagen würden sich jedoch mit den gerade hinzugefügten neuen Daten überschneiden.  
  
 Beispiele für Abfragen und weitere Informationen über die Syntax für die Verwendung von **REPLACE_MODEL_CASES** und **EXTEND_MODEL_CASES**, finden Sie unter [PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md).  
  
  
###  <a name="bkmk_EXTEND"></a> Treffen von Vorhersagen mit EXTEND_MODEL_CASES  
 Das Vorhersageverhalten unterscheidet sich abhängig davon, ob Sie die Modellfälle erweitern oder ersetzen. Wenn Sie ein Modell erweitern, werden die neuen Daten am Ende der Reihe angefügt, und die Größe des Trainingssatzes nimmt zu. Die für Vorhersageabfragen verwendeten Zeitscheiben beginnen jedoch immer am Ende der ursprünglichen Reihe. Wenn Sie also drei neue Datenpunkte hinzufügen und sechs Vorhersagen anfordern, überschneiden sich die ersten drei zurückgegebenen Vorhersagen mit den neuen Daten. In diesem Fall gibt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die tatsächlichen neuen Datenpunkte zurück und trifft keine Vorhersage, bis alle neuen Datenpunkte verwendet wurden. Danach trifft [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Vorhersagen auf Grundlage der zusammengesetzten Reihe.  
  
 Durch dieses Verhalten können Sie neue Daten hinzufügen und dann im Vorhersagediagramm die tatsächlichen Zahlen anzeigen und keine Projektionen.  
  
 Wenn Sie drei neue Datenpunkte hinzufügen und drei neue Vorhersagen treffen möchten, gehen Sie beispielsweise wie folgt vor:  
  
-   Erstellen Sie **PREDICTION JOIN** für ein Zeitreihenmodell, und geben Sie die Quelle für die neuen Daten für die drei Monate an.  
  
-   Fordern Sie Vorhersagen für sechs Zeitscheiben an. Geben Sie hierzu 6 Zeitscheiben an, wobei der Startpunkt Zeitscheibe 1 und der Endpunkt Zeitscheibe 7 ist. Dies gilt nur für EXTEND_MODEL_CASES.  
  
-   Damit nur neue Vorhersagen abgerufen werden, geben Sie als Startpunkt 4 und als Endpunkt 7 an.  
  
-   Sie müssen das Argument **EXTEND_MODEL_CASES**verwenden.  
  
     Für die ersten drei Zeitscheiben werden die tatsächlichen Umsatzzahlen zurückgegeben. Für die folgenden drei Zeitscheiben werden Vorhersagen auf Grundlage des erweiterten Modells zurückgegeben.  
  
  
###  <a name="bkmk_REPLACE"></a> Treffen von Vorhersagen mit REPLACE_MODEL_CASES  
 Wenn Sie die Fälle in einem Modell ersetzen, bleibt die Größe des Modells gleich, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ersetzt jedoch die einzelnen Fälle im Modell. Dies ist für Kreuzvorhersagen und Szenarien hilfreich, in denen das Beibehalten einer einheitlichen Größe für das Trainingsdataset wichtig ist.  
  
 Ein Beispielfall ist, dass eines Ihrer Geschäfte nicht über ausreichende Umsatzdaten verfügt. Sie könnten ein allgemeines Modell erstellen, indem Sie die durchschnittlichen Umsätze für alle Geschäfte in einer bestimmten Region ermitteln und dann ein Modell trainieren. Damit Sie mit ausreichenden Umsatzdaten Vorhersagen für das Geschäft treffen können, erstellen Sie dann **PREDICTION JOIN** mit den neuen Umsatzdaten nur für dieses Geschäft. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] behält dabei die vom regionalen Model abgeleiteten Muster bei, ersetzt jedoch die vorhandenen Trainingsfälle durch die Daten des einzelnen Geschäfts. Die Vorhersagewerte sind so näher an den Trendlinien für das einzelne Geschäft.  
  
 Wenn Sie das Argument **REPLACE_MODEL_CASES** verwenden, fügt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] kontinuierlich neue Fälle am Ende des Fallsatzes ein und löscht die entsprechende Anzahl am Anfang des Fallsatzes. Wenn Sie mehr neue Daten hinzufügen, als im ursprünglichen Trainingssatz vorhanden waren, verwirft [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die ältesten Daten. Wenn Sie genügende neue Werte angeben, können die Vorhersagen auf vollkommen neuen Daten basieren.  
  
 Angenommen, Sie haben das Modell mit einem Falldataset mit 1000 Zeilen trainiert. Anschließend fügen Sie 100 Zeilen neuer Daten hinzu. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwirft die ersten 100 Zeilen des Trainingssatzes und fügt die 100 Zeilen mit neuen Daten am Ende des Satzes ein, sodass insgesamt 1000 Zeilen vorhanden sind. Wenn Sie 1100 Zeilen mit neuen Daten hinzufügen, werden nur die letzten 1000 Zeilen verwendet.  
  
 Im Folgenden wird ein weiteres Beispiel beschrieben. Wenn Sie neue Daten für drei Monate hinzufügen und drei neue Vorhersagen treffen möchten, führen Sie die folgenden Aktionen aus:  
  
-   Erstellen Sie einen **PREDICTION JOIN** für ein Zeitreihenmodell und verwenden Sie das Argument **REPLACE_MODEL_CASE** .  
  
-   Geben Sie die Quelle der neuen Daten für drei Monate an. Diese Daten können aus einer vollkommen anderen Quelle als die ursprünglichen Trainingsdaten stammen.  
  
-   Fordern Sie Vorhersagen für sechs Zeitscheiben an. Geben Sie hierzu 6 Zeitscheiben an, oder geben Sie als Startpunkt Zeitscheibe 1 und als Endpunkt Zeitscheibe 7 an.  
  
    > [!NOTE]  
    >  Im Gegensatz zu **EXTEND_MODEL_CASES**können Sie nicht die Werte zurückgeben, die Sie als Eingabedaten hinzugefügt haben. Alle sechs zurückgegebenen Werte sind Vorhersagen auf Grundlage des aktualisierten Modells, das sowohl alte als auch neue Daten enthält.  
  
    > [!NOTE]  
    >  Wenn Sie bei REPLACE_MODEL_CASES am Timestamp 1 beginnen, erhalten Sie neue Vorhersagen basierend auf den neuen Daten, die die alten Trainingsdaten ersetzen.  
  
 Beispiele für Abfragen und weitere Informationen über die Syntax für die Verwendung von **REPLACE_MODEL_CASES** und **EXTEND_MODEL_CASES**, finden Sie unter [PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md).  
  
  
###  <a name="bkmk_MissingValues"></a> Ersetzen von fehlenden Werten in Zeitreihenmodellen  
 Wenn Sie einem Zeitreihenmodell mit einer **PREDICTION JOIN** -Anweisung neue Daten hinzufügen, darf das neue Dataset keine fehlenden Werte aufweisen. Wenn eine Reihe unvollständig ist, muss das Modell die fehlenden Werte einfügen. Dabei wird NULL, ein numerisches Mittel, ein bestimmtes numerisches Mittel oder ein Vorhersagewert verwendet. Wenn Sie **EXTEND_MODEL_CASES**angeben, ersetzt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die fehlenden Werte durch Vorhersagen auf Grundlage des ursprünglichen Modells. Wenn Sie **REPLACE_MODEL_CASES**verwenden, ersetzt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die fehlenden Werte durch den im *MISSING_VALUE_SUBSTITUTION* -Parameter angegebenen Wert.  
  
## <a name="list-of-prediction-functions"></a>Liste der Vorhersagefunktionen  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Algorithmus unterstützt jedoch die zusätzlichen Funktionen, die in der folgenden Tabelle aufgeführt sind.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[Lag &#40;DMX&#41;](../../dmx/lag-dmx.md)|Gibt eine Anzahl von Zeitscheiben zwischen dem Datum des aktuellen Falls und dem letzten Datum des Trainingssatzes zurück.<br /><br /> Diese Funktion dient in der Regel dazu, neuere Trainingsfälle zu ermitteln, sodass Sie detaillierte Daten über die Fälle abrufen können.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Gibt die Knoten-ID für die angegebene vorhersagbare Spalte zurück.<br /><br /> Diese Funktion dient gewöhnlich zum Identifizieren des Knotens, der einen bestimmten vorhergesagten Wert generiert hat, sodass Sie die mit dem Knoten verknüpften Fälle prüfen oder die Gleichung und andere Details abrufen können.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Gibt die Standardabweichung der Vorhersagen in der angegebenen vorhersagbaren Spalte zurück.<br /><br /> Diese Funktion ersetzt das INCLUDE_STATISTICS-Argument, das bei Zeitreihenmodellen nicht unterstützt wird.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Gibt die Varianz der Vorhersagen für die angegebene vorhersagbare Spalte zurück.<br /><br /> Diese Funktion ersetzt das INCLUDE_STATISTICS-Argument, das bei Zeitreihenmodellen nicht unterstützt wird.|  
|[PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md)|Gibt vorhergesagte Vergangenheits- oder Zukunftswerte für eine Zeitreihe zurück.<br /><br /> Sie können Zeitreihenmodelle auch mithilfe der allgemeinen Vorhersagefunktion [Predict &#40;DMX&#41;](../../dmx/predict-dmx.md) abfragen.|  
  
 Eine Liste der Funktionen, die von allen [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Algorithmen verwendet werden, finden Sie unter [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Die Syntax einzelner Funktionen finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Funktionsreferenz](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft Time Series-Algorithmus](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Technische Referenz für Microsoft Time Series-Algorithmus](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Miningmodellinhalt von Zeitreihenmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  

