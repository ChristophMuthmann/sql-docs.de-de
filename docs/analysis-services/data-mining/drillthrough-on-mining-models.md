---
title: "Miningmodell-Drillthrough | Microsoft Docs"
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
ms.assetid: f179a467-7d03-4d61-8e9a-6b5afb5fc2d5
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 8
---
# Miningmodell-Drillthrough
  *Drillthrough* beschreibt die Fähigkeit, entweder ein Miningmodell oder eine Miningstruktur abzufragen und ausführliche Daten zu erhalten, die im Modell nicht verfügbar sind.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bietet zwei verschiedene Optionen für Drillthroughs in Falldaten. Sie können einen Drillthrough mit den Fällen ausführen, die für die Erstellung der Daten verwendet wurden, oder Sie führen einen Drillthrough mit den Fällen in der Miningstruktur aus.  
  
## Drillthrough zu Modellfällen im Vergleich zu Drillthrough zu Strukturen  
 Ein Drillthrough zu **Modellfällen** ist hilfreich für die Suche nach weiteren Details zu Regeln, Mustern oder Clustern in einem Modell. Sie würden beispielsweise keine Kundenkontaktinformationen in einem Clustermodell für die Analyse verwenden, auch wenn Ihnen die Daten zur Verfügung stünden. Durch einen Drillthrough können Sie auf diese Informationen vom Modell zugreifen.  
  
 Demgegenüber soll ein **** Drillthrough in Bezug auf Strukturdaten einen Zugriff auf Informationen ermöglichen, die im Modell nicht verfügbar waren. Beispielsweise könnten einige Strukturspalten aus dem Modell ausgeschlossen sein, da entweder der Datentyp nicht kompatibel war oder die Daten für die Analyse nicht nützlich waren.  
  
## Ermöglichen von Drillthrough für ein Modell  
 Damit ein Drillthrough auf ein Miningmodell angewendet werden kann, müssen die folgenden Bedingungen erfüllt werden:  
  
-   Es ist zwar möglich, einen Drillthrough nur für die Modellfälle zu konfigurieren und nicht für die Miningstruktur. Dies ist aber umgekehrt nicht möglich.  Der Drillthrough muss demnach für das Miningmodell aktiviert sein, um einen Drillthrough durch die Miningstruktur zu erlauben.  
  
-   Der Drillthrough für Modell und Struktur ist standardmäßig deaktiviert. Wenn Sie den Data Mining-Assistenten verwenden, befindet sich die Option zur Aktivierung von Drillthrough für die Modellfälle auf der letzten Seite des Assistenten.  
  
-   Sie können die Drillthroughfähigkeit einem vorhandenen Miningmodell hinzufügen, in diesem Fall muss das Modell jedoch neu verarbeitet werden, bevor Sie einen Drillthrough mit den Daten ausführen.  
  
-   Der Drillthrough kann nicht ausgeführt werden, außer wenn der Cache, der während des Trainingsprozesses erstellt wurde, beibehalten wurde. Weitere Informationen zu den Eigenschaften zur Steuerung der Zwischenspeicherung finden Sie unter [Drillthrough in Miningstrukturen](../../analysis-services/data-mining/drillthrough-on-mining-structures.md).  
  
## Modelle, die Drillthrough unterstützen  
 Wenn ein Miningmodell für die Verwendung von Drillthrough konfiguriert wurde, und wenn Sie über die erforderlichen Berechtigungen verfügen, können Sie beim Durchsuchen eines Modells im entsprechenden Viewer auf einen Knoten klicken, und detaillierte Informationen über die Fälle in diesem bestimmten Knoten abrufen.  
  
 Nicht alle Modelle unterstützen Drillthrough. Dies hängt vom Algorithmus ab, der verwendet wurde, um das Modell zu erstellen. In der folgenden Tabelle sind die Modelltypen aufgeführt, die Drillthrough nicht oder nur mit Einschränkungen unterstützen. Wenn der Modelltyp hier nicht aufgeführt ist, wird Drillthrough unterstützt.  
  
|**Algorithmusname**|**Unterstützung für Drillthrough**|  
|------------------------|----------------------------------|  
|Microsoft Naive Bayes-Algorithmus|Nicht unterstützt.<br /><br /> Diese Algorithmen weisen bestimmten Knoten im Inhalt keine Fälle zu.|  
|Microsoft Neural Network-Algorithmus|Nicht unterstützt.<br /><br /> Diese Algorithmen weisen bestimmten Knoten im Inhalt keine Fälle zu.|  
|Microsoft Logistic Regression-Algorithmus|Nicht unterstützt.<br /><br /> Diese Algorithmen weisen bestimmten Knoten im Inhalt keine Fälle zu.|  
|Microsoft Linear Regression-Algorithmus|Unterstützt.<br /><br /> Da das Modell jedoch als einzigen Knoten **All**erstellt, gibt Drillthrough alle Trainingsfälle des Modells zurück. Bei einem großen Trainingssatz kann es sehr lange dauern, bis die Ergebnisse geladen werden.|  
|Microsoft Time Series-Algorithmus|Unterstützt.<br /><br /> Sie können jedoch keinen Drillthrough mit Struktur- oder Falldaten unter Verwendung des **Miningmodell-Viewers** im Data Mining-Designer ausführen. Sie müssen stattdessen eine DMX-Abfrage erstellen.<br /><br /> Sie können außerdem keinen Drillthrough auf bestimmten Knoten ausführen oder DMX-Abfragen schreiben, um Fälle von bestimmten Knoten eines Zeitreihenmodells abzurufen. Sie können Falldaten entweder aus dem Modell oder aus der Struktur abrufen, indem Sie andere Kriterien verwenden, beispielsweise Datums- oder Attributwerte.<br /><br /> Wenn Sie Details der vom Microsoft Time Series-Algorithmus erstellten ARTXP- und ARIMA-Knoten anzeigen möchten, empfiehlt es sich, den [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md) zu verwenden.|  
  
## Verwandte Aufgaben  
 In den folgenden Themen finden Sie weitere Informationen zur Verwendung von Drillthroughs mit Miningmodellen.  
  
|Aufgaben|Links|  
|-----------|-----------|  
|Verwenden von Drillthrough in den Miningmodell-Viewern|[Verwenden von Drillthrough mit den Modell-Viewern](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|Abrufen von Falldaten für ein Modell mithilfe von Drillthrough|[Ausführen von Drillthroughs für Falldaten aus einem Miningmodell](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|Aktivieren von Drillthrough für ein vorhandenes Miningmodell|[Aktivieren von Drillthrough für ein Miningmodell](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|In Beispielen von Drillthroughabfragen finden Sie Informationen zu bestimmten Modelltypen.|[Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)|  
|Aktivieren von Drillthrough im Miningmodell-Assistenten|[Abschließen des Assistenten &#40;Data Mining-Assistent&#41;](../Topic/Completing%20the%20Wizard%20\(Data%20Mining%20Wizard\).md)|  
  
## Siehe auch  
 [Drillthrough in Miningstrukturen](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  