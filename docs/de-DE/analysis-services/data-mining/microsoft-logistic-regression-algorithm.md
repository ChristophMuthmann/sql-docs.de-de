---
title: Microsoft Logistic Regression-Algorithmus | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logical regression algorithms [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dd07a9b2b56393e18f7115f3caf8e251b3f9572f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-logistic-regression-algorithm"></a>Microsoft Logistic Regression-Algorithmus
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Die logistische Regression ist ein gängiges statistisches Verfahren, das zum Modellieren von binären Ergebnissen verwendet wird.  
  
 Es gibt in der Statistikforschung verschiedene Implementierungen einer logistischen Regression, die unterschiedliche Lerntechniken verwenden. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Logistic Regression-Algorithmus wurde basierend auf einer Variation des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus implementiert. Dieser Algorithmus weist viele der Qualitäten neuronaler Netzwerke auf, ist jedoch einfacher zu trainieren.  
  
 Ein Vorteil des logistischen Regressionsalgorithmus ist seine Flexibilität. Er akzeptiert alle Arten von Eingaben und unterstützt verschiedene analytische Tasks:  
  
-   Verwenden Sie demografische Daten, um Vorhersagen zu Ergebnissen zu treffen, z. B. zum Risiko einer bestimmten Krankheit.  
  
-   Untersuchen und gewichten Sie die Faktoren, die zu einem Ergebnis beitragen. Suchen Sie z. B. nach den Faktoren, die Kunden dazu veranlassen, einem Geschäft einen zweiten Besuch abzustatten.  
  
-   Klassifizieren Sie Dokumente, E-Mails oder andere Objekte, die über viele Attribute verfügen.  
  
## <a name="example"></a>Beispiel  
 Stellen Sie sich eine Gruppe von Personen vor, die ähnliche demografische Daten aufweisen und Produkte der Firma Adventure Works kaufen. Indem Sie die Daten so modellieren, dass sie sich auf ein bestimmtes Ergebnis beziehen, z. B. auf den Kauf eines Zielprodukts, können Sie ermitteln, wie die demografischen Daten sich bei einem Käufer auf die Wahrscheinlichkeit auswirken, dass dieser das Zielprodukt kauft.  
  
## <a name="how-the-algorithm-works"></a>Funktionsweise des Algorithmus  
 Die logistische Regression ist ein gängiges statistisches Verfahren, mit dem der Beitrag mehrerer Faktoren zu zwei bestimmten Ergebnissen ermittelt werden kann. Die Microsoft-Implementierung verwendet ein modifiziertes neuronales Netzwerk, um die Beziehungen zwischen Eingaben und Ausgaben zu modellieren. Es wird jeweils die Auswirkung jeder Eingabe auf die Ausgabe gemessen, und im fertigen Modell werden die verschiedenen Eingaben gewichtet. Der Name "Logistische Regression" beruht auf der Tatsache, dass die Datenkurve mithilfe einer logistischen Transformation komprimiert wird, um die Auswirkungen extremer Werte zu minimieren. Weitere Informationen zur Implementierung und dazu, wie der Algorithmus angepasst wird, finden Sie unter [Technische Referenz für den Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## <a name="data-required-for-logistic-regression-models"></a>Erforderliche Daten für logistische Regressionsmodelle  
 Wenn Sie Daten für das Training eines logistischen Regressionsmodells aufbereiten, müssen Sie sich mit den Anforderungen des jeweiligen Algorithmus, dessen Anforderungen an die Daten und der Verwendung der Daten vertraut machen.  
  
 Für ein logistisches Regressionsmodell gelten folgende Anforderungen:  
  
 **Nur eine Schlüsselspalte:** Jedes Modell muss eine numerische Spalte oder Textspalte enthalten, die jeden Datensatz eindeutig identifiziert. Verbundschlüssel sind nicht zulässig.  
  
 **Eingabespalten:** Jedes Modell muss mindestens eine Eingabespalte für die Werte enthalten, die bei der Analyse als Faktoren verwendet werden. Sie können beliebig viele Eingabespalten verwenden. Abhängig von der Anzahl von Werten in jeder Spalte, kann sich der zum Trainieren des Modells erforderliche Zeitaufwand durch das Hinzufügen zusätzlicher Spalten jedoch erhöhen.  
  
 **Mindestens eine vorhersagbare Spalte:** Das Modell muss mindestens eine vorhersagbare Spalte eines beliebigen Datentyps enthalten, einschließlich fortlaufender numerischer Daten. Die Werte der vorhersagbaren Spalte können auch als Eingaben für das Modell behandelt werden. Alternativ dazu können Sie angeben, dass diese Werte nur für Vorhersagen verwendet werden sollen. Geschachtelte Tabellen sind für vorhersagbare Spalten nicht zulässig, können aber als Eingaben verwendet werden.  
  
 Ausführliche Informationen zu den in logistischen Regressionsmodellen unterstützten Inhaltstypen und Datentypen finden Sie im Abschnitt über Anforderungen unter [Technische Referenz für den Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## <a name="viewing-a-logistic-regression-model"></a>Anzeigen eines logistischen Regressionsmodells  
 Zum Untersuchen des Modells können Sie den Microsoft-Viewer für neuronale Netzwerke oder den Microsoft Generic Content Tree Viewer verwenden.  
  
 Wenn Sie das Modell mit dem Microsoft-Viewer für neuronale Netzwerke anzeigen, führt Analysis Services die Faktoren, die zu einem bestimmten Ergebnis beitragen, nach ihrer Wichtigkeit auf. Sie können ein Attribut und Werte für einen Vergleich auswählen. Weitere Informationen finden Sie unter [Modell mit dem Microsoft-Viewer für neuronale Netzwerke durchsuchen](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Wenn Sie ausführlichere Informationen benötigen, können Sie mit dem Microsoft Generic Content Tree Viewer die Details des Modells durchsuchen. Der Modellinhalt für ein logistisches Regressionsmodell enthält einen Knoten für die Randstatistik, der alle für das Modell verwendeten Eingaben und die Subnetzwerke für die vorhersagbaren Attribute anzeigt. Weitere Informationen finden Sie unter [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md).  
  
## <a name="creating-predictions"></a>Erstellen von Vorhersagen  
 Nachdem das Training für das Modell durchgeführt wurde, können Sie für den Modellinhalt Abfragen erstellen, um die Regressionskoeffizienten und andere Details abzurufen, oder Sie können das Modell verwenden, um Vorhersagen zu erstellen.  
  
-   Allgemeine Informationen zur Erstellung von Abfragen für ein Data Mining-Modell finden Sie unter [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md).  
  
-   Beispiele für Abfragen in Verbindung mit einem logistischen Regressionsmodell finden Sie unter [Beispiele für Clusteringmodellabfragen](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Hinweise  
  
-   Unterstützt keine Drillthroughs. Der Grund hierfür ist, dass die Struktur der Knoten im Miningmodell nicht zwangsläufig direkt den zugrunde liegenden Daten entspricht.  
  
-   Unterstützt nicht die Erstellung von Data Mining-Dimensionen.  
  
-   Unterstützt die Verwendung von OLAP-Miningmodellen.  
  
-   Unterstützt nicht die Verwendung von PMML (Predictive Model Markup Language) zum Erstellen von Miningmodellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [Technische Referenz zu Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Beispiele für logistische Regressionsmodellabfragen](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)  
  
  
