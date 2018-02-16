---
title: Technische Referenz zu Microsoft Linear Regression-Algorithmus | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2ad96596830cc3bb091a7f57639c0a7d0d84dd9c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Technische Referenz für den Microsoft Linear Regression-Algorithmus
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus ist eine spezielle Version des Microsoft Decision Trees-Algorithmus, der für die Modellierung kontinuierlicher Attributpaare optimiert ist. In diesem Thema wird die Implementierung des Algorithmus erläutert und beschrieben, wie das Verhalten des Algorithmus angepasst wird. Ferner werden Links zu weiteren Informationen über das Abfragen von Modellen zur Verfügung gestellt.  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>Implementierung des Linear Regression-Algorithmus  
 Der Microsoft Decision Trees-Algorithmus kann für viele Tasks verwendet werden: die lineare Regression, die Klassifizierung oder die Zuordnungsanalyse. Um diesen Algorithmus für die lineare Regression zu implementieren, werden die Parameter des Algorithmus gesteuert, um die Zunahme der Struktur zu beschränken und alle Daten im Modell in einem einzigen Knoten zu speichern. Mit anderen Worten, obwohl die lineare Regression auf einer Entscheidungsstruktur basiert, enthält die Struktur nur einen einzigen Stamm und keine Verzweigungen: Alle Daten befinden sich im Stammknoten.  
  
 Um dies zu erreichen, ist der *MINIMUM_LEAF_CASES* -Parameter größer als oder gleich der Gesamtzahl der Fälle im Dataset, mit dem der Algorithmus das Miningmodell trainiert. Bei dieser Parametereinstellung erstellt der Algorithmus nie eine Teilung, was der Grund dafür ist, dass der Algorithmus eine lineare Regression ausführt.  
  
 Die Gleichung, die die Regressionsgleichung darstellt, weist im Allgemeinen die Form „y = ax + b“ auf und wird als Regressionsgleichung bezeichnet. Die Variable Y stellt die Ausgabevariable dar, X stellt die Eingabevariable dar, und a und b sind anpassbare Koeffizienten. Sie können die Koeffizienten, Achsenabschnitte und andere Informationen über die Regressionsformel abrufen, indem Sie das fertige Miningmodell abfragen. Weitere Informationen finden Sie unter [Beispiele für lineare Regressionsmodellabfrage](../../analysis-services/data-mining/linear-regression-model-query-examples.md).  
  
### <a name="scoring-methods-and-feature-selection"></a>Bewertungsmethoden und Funktionsauswahl  
 Die Funktionsauswahl wird automatisch von allen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining-Algorithmen zur Verbesserung der Analyse und zur Reduzierung der Verarbeitungslast verwendet. Die für die Funktionsauswahl bei der linearen Regression verwendete Methode ist der Interessantheitsgrad, da das Modell nur kontinuierliche Spalten unterstützt. Die folgende Tabelle zeigt zu Referenzzwecken den Unterschied bei der Funktionsauswahl für den Linear Regression-Algorithmus und den Decision Trees-Algorithmus.  
  
|Algorithmus|Analysemethode|Kommentare|  
|---------------|------------------------|--------------|  
|Lineare Regression|Interessantheitsgrad|Standard.<br /><br /> Andere Funktionsauswahlmethoden, die für den Decision Trees-Algorithmus verfügbar sind, sind nur für diskrete Variablen gültig und gelten daher nicht für lineare Regressionsmodelle.|  
|Entscheidungsstrukturen|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Wenn irgendeine Spalte nicht binäre kontinuierliche Werte enthält, wird der Interessantheitsgrad für alle Spalten verwendet, um die Konsistenz zu gewährleisten. Andernfalls wird die Standardmethode oder die angegebene Methode verwendet.|  
  
 Die Algorithmusparameter, die die Funktionsauswahl für ein Entscheidungsstrukturmodell steuern, sind MAXIMUM_INPUT_ATTRIBUTES und MAXIMUM_OUTPUT.  
  
## <a name="customizing-the-linear-regression-algorithm"></a>Anpassen des Linear Regression-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus unterstützt Parameter, die Auswirkungen auf das Verhalten, die Leistung und die Genauigkeit des resultierenden Miningmodells haben. Sie können außerdem Modellierungsflags für die Miningmodellspalten oder Miningstrukturspalten festlegen, um die Verarbeitung der Daten zu steuern.  
  
### <a name="setting-algorithm-parameters"></a>Festlegen von Algorithmusparametern  
 In der folgenden Tabelle werden die Parameter, die für den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus bereitgestellt werden, aufgelistet.  
  
|Parameter|Description|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|Definiert die Anzahl von Eingabeattributen, die der Algorithmus verarbeiten kann, bevor die Funktionsauswahl aufgerufen wird. Legen Sie diesen Wert auf 0 fest, um die Funktionsauswahl zu deaktivieren.<br /><br /> Der Standardwert lautet 255.|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|Definiert die Anzahl von Ausgabeattributen, die der Algorithmus verarbeiten kann, bevor die Funktionsauswahl aufgerufen wird. Legen Sie diesen Wert auf 0 fest, um die Funktionsauswahl zu deaktivieren.<br /><br /> Der Standardwert lautet 255.|  
|*FORCE_REGRESSOR*|Zwingt den Algorithmus, die angegebenen Spalten als Regressoren zu verwenden, und zwar unabhängig von ihrer durch den Algorithmus berechneten Bedeutung.|  
  
### <a name="modeling-flags"></a>Modellierungsflags  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus unterstützt die folgenden Modellierungsflags. Wenn Sie die Miningstruktur oder das Miningmodell erstellen, definieren Sie Modellierungsflags, die angeben, wie die Werte in den einzelnen Spalten während der Analyse behandelt werden. Weitere Informationen finden Sie unter [Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Modellierungsflag|Description|  
|-------------------|-----------------|  
|NOT NULL|Gibt an, dass die Spalte keinen NULL-Wert enthalten kann. Ein Fehler tritt auf, wenn Analysis Services während des Modelltrainings einen NULL-Wert erkennt.<br /><br /> Gilt für die Miningstrukturspalten.|  
|REGRESSOR|Gibt an, dass die Spalte kontinuierliche numerische Werte enthält, die bei der Analyse als potenzielle unabhängige Variablen behandelt werden sollen. Gilt für die Miningmodellspalten.<br /><br /> Hinweis: Das Kennzeichnen einer Spalte als Regressor gewährleistet nicht, dass die Spalte im fertigen Modell als Regressor verwendet wird.|  
  
### <a name="regressors-in-linear-regression-models"></a>Regressoren in linearen Regressionsmodellen  
 Lineare Regressionsmodelle basieren auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus. Auch wenn Sie den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus nicht verwenden, kann jedes Entscheidungsstrukturmodell eine Struktur oder Knoten enthalten, die eine Regression für ein kontinuierliches Attribut darstellen.  
  
 Sie müssen nicht angeben, dass eine kontinuierliche Spalte einen Regressor darstellt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus unterteilt das Dataset selbst dann in Bereiche mit sinnvollen Mustern, wenn Sie das REGRESSOR-Flag nicht für die Spalte festlegen. Der Unterschied besteht darin, dass der Algorithmus beim Festlegen des Modellierungsflags versucht, Regressionsgleichungen im Format `a*C1 + b*C2 + ...` entsprechend den Mustern in den Knoten der Struktur zu finden. Dann wird die Summe der Restwerte berechnet, und wenn die Abweichung zu groß ist, wird die Struktur unterteilt.  
  
 Wenn Sie beispielsweise das Kaufverhalten von Kunden mithilfe des Attributs „Income“ vorhersagen und das REGRESSOR-Modellierungsflag für die Spalte „[Income]“ festlegen, versucht der Algorithmus zuerst, die Werte mithilfe einer Standardregressionsformel zuzuordnen. Ist die Abweichung zu groß, dann wird die Regressionsformel ignoriert und die Struktur nach einem anderen Attribut unterteilt. Der Decision Tree-Algorithmus versucht nach der Unterteilung, jedem der Zweige einen Regressor für Income zuzuordnen.  
  
 Sie können durch Einsatz des FORCED_REGRESSOR-Parameters gewährleisten, dass der Algorithmus einen bestimmten Regressor verwendet. Dieser Parameter kann mit dem Microsoft Decision Trees-Algorithmus und dem Microsoft Linear Regression-Algorithmus verwendet werden.  
  
## <a name="requirements"></a>Anforderungen  
 Ein lineares Regressionsmodell muss eine Schlüsselspalte, Eingabespalten und mindestens eine vorhersagbare Spalte enthalten.  
  
### <a name="input-and-predictable-columns"></a>Eingabespalten und vorhersagbare Spalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus unterstützt bestimmte Eingabespalten und vorhersagbare Spalten. Diese sind in der nachstehenden Tabelle aufgelistet. Weitere Informationen zur Bedeutung der Inhaltstypen in einem Miningmodell finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Column|Inhaltstypen|  
|------------|-------------------|  
|Eingabeattribut|Continuous, Cyclical, Key, Table und Ordered|  
|Vorhersagbares Attribut|Continuous, Cyclical und Ordered|  
  
> [!NOTE]  
>  Die Inhaltstypen**Cyclical** und **Ordered** werden unterstützt, der Algorithmus behandelt sie jedoch als diskrete Werte und führt keine spezielle Verarbeitung durch.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Linear Regression-Algorithmus](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [Lineare Regressionsmodell-Abfragebeispiele](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [Miningmodellinhalt, lineare Regressionsmodelle &#40; Analysis Services – Datamining &#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
