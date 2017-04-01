---
title: "Logistische Regressionsmodell-Abfragebeispiele | Microsoft Docs"
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
  - "logistische Regression [Analysis Services]"
  - "Inhaltsabfragen [DMX]"
ms.assetid: 7c8e13a3-5c67-46c2-abfa-4881e6ef9c62
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 22
---
# Logistische Regressionsmodell-Abfragebeispiele
  Beim Generieren einer Abfrage für ein Data Mining-Modell können Sie eine Inhaltsabfrage erstellen, die Details über die bei der Analyse ermittelten Muster liefert. Alternativ dazu können Sie auch eine Vorhersageabfrage erstellen, die Vorhersagen mit neuen Daten anhand der im Modell befindlichen Muster vornimmt.  
  
 In diesem Abschnitt wird erläutert, wie diese beiden Abfragetypen für Modelle erstellt werden, die auf dem Microsoft Logistic Regression-Algorithmus basieren.  
  
 **Inhaltsabfragen**  
  
 [Abrufen von Modellparametern mithilfe des Data Mining-Schemarowsets](#bkmk_Query1)  
  
 [Ermittlung weiterer Details des Modells mit DMX](#bkmk_Query2)  
  
 **Vorhersageabfragen**  
  
 [Erstellen von Vorhersagen für einen kontinuierlichen Wert](#bkmk_Query3)  
  
 [Erstellen von Vorhersagen für einen diskreten Wert](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> Abrufen von Informationen zum logistischen Regressionsmodell  
 Logistische Regressionsmodelle werden mithilfe des Microsoft Neural Network-Algorithmus mit einer speziellen Menge von Parametern erstellt. Daher verfügt das logistische Regressionsmodell über einige der Informationen, die auch das neuronale Netzwerk enthält, ist jedoch weniger komplex. Weitere Informationen zur Struktur des Inhaltsmodells und dazu, in welchen Knotentypen welche Arten von Informationen gespeichert sind, finden Sie unter [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining model content for logistic regression models.md).  
  
 Für die Abfrageszenarios können Sie ein logistisches Regressionsmodell erstellen, wie im folgenden Abschnitt des Data Mining-Tutorials für Fortgeschrittene beschrieben: [Lektion 5: Erstellen von neuronalen Netzwerk- und logistischen Regressionsmodellen &#40;Data Mining-Tutorial für Fortgeschrittene&#41;](../Topic/Lesson%205:%20Building%20Neural%20Network%20and%20Logistic%20Regression%20Models%20\(Intermediate%20Data%20Mining%20Tutorial\).md).  
  
 Sie können auch die Miningstruktur Targeted Mailing aus dem [Tutorial zu Data Mining-Grundlagen](../Topic/Basic%20Data%20Mining%20Tutorial.md) verwenden.  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Abrufen von Modellparametern mithilfe des Data Mining-Schemarowsets  
 Durch Abfrage des Data Mining-Schemarowsets können Sie Metadaten zum Modell ermitteln, wie das Datum der Modellerstellung, das Datum der letzten Modellverarbeitung, den Namen der Miningstruktur, auf der das Modell basiert, und den Namen der als vorhersagbares Attribut verwendeten Spalte. Mit dem folgenden Beispiel werden die Parameter zurückgegeben, die beim Erstellen des Modells verwendet wurden, sowie Name und Typ des Modells und das Datum, an dem es erstellt wurde.  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 Beispielergebnisse:  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Ermittlung weiterer Details des Modells mit DMX  
 Die folgende Abfrage gibt einige grundlegende Informationen über das logistische Regressionsmodell zurück. Ein logistisches Regressionsmodell ähnelt in vielerlei Hinsicht einem neuronalen Netzwerkmodell. Dazu gehört das Vorhandensein eines Knotens für Randstatistik (NODE_TYPE = 24), der die als Eingaben verwendeten Werte beschreibt. in dieser Beispielabfrage wird das Targeted Mailing-Modell verwendet, und die Werte aller Eingaben werden aus der geschachtelten Tabelle NODE_DISTRIBUTION abgerufen.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 Teilergebnisse:  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Age|Nicht vorhanden|0|0|0|1|  
|Age|45.43491192|17484|1|126.9544114|3|  
|Bike Buyer|Nicht vorhanden|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Commute Distance|Nicht vorhanden|0|0|0|1|  
|Commute Distance|5–10 Meilen|3033|0,173472889|0|4|  
  
 Die eigentliche Abfrage gibt weitaus mehr Zeilen zurück. Dieses Beispiel veranschaulicht jedoch die Art der Informationen, die über Eingaben zur Verfügung gestellt werden. Für diskrete Eingaben wird jeder mögliche Wert in der Tabelle aufgeführt. Für Eingaben mit kontinuierlichen Werten wie Age ist eine vollständige Auflistung unmöglich, daher wird die Eingabe als Mittelwert diskretisiert. Weitere Informationen dazu, wie Sie die Informationen im Knoten Randstatistik verwenden, finden Sie unter [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining model content for logistic regression models.md).  
  
> [!NOTE]  
>  Die Ergebnisse wurden zugunsten einer leichteren Anzeige vereinfacht. Sie können die geschachtelte Tabelle jedoch in einer einzelnen Spalte zurückgeben, wenn Ihr Anbieter hierarchische Rowsets unterstützt.  
  
## Vorhersageabfragen eines logistischen Regressionsmodells  
 Sie können die Funktion [Predict &#40;DMX&#41;](../../dmx/predict-dmx.md) mit jeder Art von Miningmodell verwenden, um neue Daten für das Modell zur Verfügung zu stellen und Vorhersagen anhand der neuen Werte zu treffen. Außerdem können Sie mithilfe von Funktionen weitere Informationen über die Vorhersage zurückgeben, z. B. die Wahrscheinlichkeit, dass eine Vorhersage zutrifft. Dieser Abschnitt enthält einige Beispiele für Vorhersageabfragen für ein logistisches Regressionsmodell.  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Erstellen von Vorhersagen für einen kontinuierlichen Wert  
 Da die logistische Regression die Verwendung kontinuierlicher Attribute sowohl für die Eingabe als auch die Vorhersage unterstützt, können ganz einfach Modelle erstellt werden, die verschiedene Faktoren in Ihren Daten korrelieren. Sie können Vorhersageabfragen verwenden, um das Beziehungsgefüge dieser Faktoren zu erforschen.  
  
 Das folgende Abfragebeispiel basiert auf dem Callcentermodell aus dem Lernprogramm für Fortgeschrittene. Darin wird eine SINGLETON-Abfrage erstellt, die die Dienstqualität für die Schicht "Friday AM" vorhersagt. Die Funktion [PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md) gibt eine geschachtelte Tabelle mit statistischen Daten zurück, die für das Verständnis der Gültigkeit des vorhergesagten Werts relevant sind.  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 Beispielergebnisse:  
  
|Predicted Service Grade|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-----------------------------|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
|||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 Weitere Informationen zu Wahrscheinlichkeit, Unterstützung und Standardabweichung der Werte in der geschachtelten NODE_DISTRIBUTION-Tabelle finden Sie unter [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining model content for logistic regression models.md).  
  
###  <a name="bkmk_Query4"></a> Beispielabfrage 4: Erstellen von Vorhersagen für einen diskreten Wert  
 Die logistische Regression wird normalerweise in Szenarien verwendet, in denen die Faktoren analysiert werden sollen, die zu einem binären Ergebnis beitragen. Obwohl das im Tutorial verwendete Modell den kontinuierlichen Wert **ServiceGrade** in einem realistischen Szenario vorhersagt, möchten Sie möglicherweise das Modell für die Vorhersage einrichten, ob die Dienstqualität einem bestimmten diskretisierten Zielwert entsprochen hat. Alternativ könnten Sie die Vorhersagen mit einem kontinuierlichen Wert ausgeben, später jedoch die vorhergesagten Ergebnisse in **Gut**, **Durchschnittlich**oder **Schlecht**gruppieren.  
  
 Das folgende Beispiel veranschaulicht, wie die Methode zum Gruppieren des vorhersagbaren Attributs geändert wird. Erstellen Sie hierzu eine Kopie der Miningstruktur, und ändern Sie dann die Diskretisierungsmethode der Zielspalte, damit die Werte gruppiert werden anstatt kontinuierlich sind.  
  
 Im folgenden Verfahren wird beschrieben, wie die Gruppierung von ServiceGrade-Werten in den Callcenterdaten geändert wird.  
  
##### So erstellen Sie eine diskretisierte Version der Callcenter-Miningstruktur und -Modelle  
  
1.  Erweitern Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Projektmappen-Explorer **Miningstrukturen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf „Call Center.dmm“, und wählen Sie **Kopieren** aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Miningstrukturen** , und wählen Sie **Einfügen**aus. Eine neue Miningstruktur mit dem Namen „Call Center 1“ wird hinzugefügt.  
  
4.  Klicken Sie mit der rechten Maustaste auf die neue Miningstruktur, und wählen Sie **Umbenennen** aus. Geben Sie den neuen Namen **Callcenter diskretisiert**ein.  
  
5.  Doppelklicken Sie auf die neue Miningstruktur, um sie im Designer zu öffnen. Beachten Sie, dass auch alle Miningmodelle kopiert wurden und die Erweiterung "1" haben. Ändern Sie die Namen zunächst nicht.  
  
6.  Klicken Sie auf der Registerkarte **Miningstruktur** mit der rechten Maustaste auf die Spalte für ServiceGrade, und wählen Sie **Eigenschaften** aus.  
  
7.  Ändern Sie die **Content** -Eigenschaft von **Kontinuierlich** in **Diskretisiert**. Ändern Sie die **DiscretizationMethod** -Eigenschaft in **Cluster**. Geben Sie für DiscretizationBucketCount **3**ein.  
  
    > [!NOTE]  
    >  Diese Parameter werden nur zur Veranschaulichung des Vorgangs verwendet und erzeugen nicht unbedingt ein gültiges Modell.  
  
8.  Klicken Sie im Menü **Miningmodell** auf **Miningstruktur und alle Modelle verarbeiten**.  
  
 Die folgende Beispielabfrage basiert auf diesem diskretisierten Modell und sagt die Dienstqualität für den angegebenen Wochentag sowie die Wahrscheinlichkeit für jedes vorhergesagte Ergebnis vorher.  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 Erwartete Ergebnisse:  
  
 **Vorhersagen (Predictions):**  
  
|Service Grade|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 Beachten Sie, dass die vorhergesagten Ergebnisse wie angegeben in drei Kategorien gruppiert wurden. Diese Gruppierungen basieren jedoch auf dem Clustering der Istwerte in den Daten, nicht möglicherweise als Geschäftsziele festgelegter beliebiger Werte.  
  
## Liste der Vorhersagefunktionen  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Logistic Regression-Algorithmus unterstützt jedoch zusätzliche Funktionen, die in der folgenden Tabelle aufgelistet sind.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Bestimmt, ob ein Knoten ein untergeordnetes Element eines anderen Knotens im Modell ist.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Gibt die angepasste Wahrscheinlichkeit für einen bestimmten Status zurück.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Gibt einen vorhergesagten Wert oder eine Gruppe von Werten für eine angegebene Spalte zurück.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für einen bestimmten Status zurück.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Gibt die Standardabweichung für den prognostizierten Wert zurück.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Gibt den Unterstützungswert für einen bestimmten Status zurück.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Gibt die Varianz einer angegebenen Spalte zurück.|  
  
 Eine Liste der Funktionen, die von allen [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Algorithmen verwendet werden, finden Sie unter [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Die Syntax einzelner Funktionen finden Sie unter [Data Mining-Erweiterungen – Funktionsreferenz &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
> [!NOTE]  
>  Für neuronale Netzwerk- und logistische Regressionsmodelle gibt die Funktion [PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md) einen einzelnen Wert zurück, der die Größe des Trainingssatzes für das gesamte Modell repräsentiert.  
  
## Siehe auch  
 [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Technische Referenz für den Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining model content for logistic regression models.md)   
 [Lektion 5: Erstellen von neuronalen Netzwerk- und logistischen Regressionsmodellen &#40;Data Mining-Tutorial für Fortgeschrittene&#41;](../Topic/Lesson%205:%20Building%20Neural%20Network%20and%20Logistic%20Regression%20Models%20\(Intermediate%20Data%20Mining%20Tutorial\).md)  
  
  