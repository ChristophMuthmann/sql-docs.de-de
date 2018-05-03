---
title: Miningmodellinhalt, lineare Regressionsmodell für | Microsoft Docs
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
- linear regression algorithms [Analysis Services]
- mining model content, linear regression models
- regression algorithms [Analysis Services]
ms.assetid: a6abcb75-524e-4e0a-a375-c10475ac0a9d
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 58fa05a49598019abdc7c5d452d027a4c1552672
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mining-model-content-for-linear-regression-models-analysis-services---data-mining"></a>Miningmodellinhalt von linearen Regressionsmodellen (Analysis Services – Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In diesem Thema wird der Miningmodellinhalt beschrieben, der Modellen eigen ist, die den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus verwenden. Eine Erläuterung der allgemeinen Miningmodellinhalte, die für alle Modelltypen gelten, finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-linear-regression-model"></a>Grundlegendes zur Struktur von linearen Regressionsmodellen  
 Ein lineares Regressionsmodell verfügt über eine äußerst einfache Struktur. Jedes Modell verfügt über einen einzelnen übergeordneten Knoten, der das Modell und seine Metadaten darstellt, und über einen Regressionsstrukturknoten (NODE_TYPE = 25), der die Regressionsformel für jedes vorhersagbare Attribut enthält.  
  
 ![Struktur des Modells für die lineare Regression](../../analysis-services/data-mining/media/modelcontentstructure-linreg.gif "Struktur des Modells für die lineare Regression")  
  
 Lineare Regressionsmodelle verwenden den gleichen Algorithmus wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Entscheidungsstrukturen. Allerdings kommen andere Parameter für die Einschränkung der Struktur zum Einsatz und es sind nur kontinuierliche Attribute als Eingaben zulässig. Da lineare Regressionsmodelle jedoch auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus basieren, werden lineare Regressionsmodelle mithilfe des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Entscheidungsstruktur-Viewers (Decision Tree Viewer) angezeigt. Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Struktur-Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md).  
  
 Der nächste Abschnitt erklärt, wie Informationen im Regressionsformelknoten interpretiert werden. Diese Informationen gelten nicht nur für lineare Regressionsmodelle, sondern auch für Entscheidungsstrukturmodelle, die in einem Teil der Struktur Regressionen enthalten.  
  
## <a name="model-content-for-a-linear-regression-model"></a>Modellinhalt eines linearen Regressionsmodells  
 In diesem Abschnitt werden nur diejenigen Spalten des Miningmodellinhalts detaillierter und anhand von Beispielen erläutert, die für die lineare Regression relevant sind.  
  
 Informationen zu allgemeinen Spalten im Schemarowset finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Name der Datenbank, in der das Modell gespeichert wird.  
  
 MODEL_NAME  
 Name des Modells.  
  
 ATTRIBUTE_NAME  
 **Stammknoten:** Leer  
  
 **Regressionsknoten:** Der Name des vorhersagbaren Attributs.  
  
 NODE_NAME  
 Entspricht immer NODE_UNIQUE_NAME.  
  
 NODE_UNIQUE_NAME  
 Ein innerhalb des Modells eindeutiger Bezeichner für den Knoten. Dieser Wert kann nicht geändert werden.  
  
 NODE_TYPE  
 Ein lineares Regressionsmodell gibt die folgenden Knotentypen aus:  
  
|Knotentyp-ID|Typ|Description|  
|------------------|----------|-----------------|  
|25|Regressionsstrukturstamm|Enthält die Formel, die die Beziehung zwischen der Eingabe- und der Ausgabevariablen beschreibt.|  
  
 NODE_CAPTION  
 Eine Bezeichnung oder Beschriftung, die dem Knoten zugeordnet ist. Diese Eigenschaft dient hauptsächlich zu Anzeigezwecken.  
  
 **Stammknoten:** Leer  
  
 **Regressionsknoten:** Alle.  
  
 CHILDREN_CARDINALITY  
 Eine Schätzung der Anzahl untergeordneter Elemente des Knotens.  
  
 **Stammknoten:** Weist auf die Anzahl der Regressionsknoten hin. Ein Regressionsknoten wird für jedes vorhersagbare Attribut im Modell erstellt.  
  
 **Regressionsknoten:** Immer 0.  
  
 PARENT_UNIQUE_NAME  
 Der eindeutige Name des dem Knoten übergeordneten Elements. Für Knoten auf der Stammebene wird NULL zurückgegeben.  
  
 NODE_DESCRIPTION  
 Eine Beschreibung des Knotens.  
  
 **Stammknoten:** Leer  
  
 **Regressionsknoten:** Alle.  
  
 NODE_RULE  
 Wird für lineare Regressionsmodelle nicht verwendet.  
  
 MARGINAL_RULE  
 Wird für lineare Regressionsmodelle nicht verwendet.  
  
 NODE_PROBABILITY  
 Die diesem Knoten zugeordnete Wahrscheinlichkeit.  
  
 **Stammknoten:** 0  
  
 **Regressionsknoten:** 1  
  
 MARGINAL_PROBABILITY  
 Die Wahrscheinlichkeit für das Erreichen des Knotens vom übergeordneten Knoten aus.  
  
 **Stammknoten:** 0  
  
 **Regressionsknoten:** 1  
  
 NODE_DISTRIBUTION  
 Eine geschachtelte Tabelle, die Statistiken über die Werte im Knoten bereitstellt.  
  
 **Stammknoten:** 0  
  
 **Regressionsknoten:** Eine Tabelle, die die Elemente enthält, die verwendet werden, um die Regressionsformel zu erstellen. Ein Regressionsknoten enthält die folgenden Werttypen:  
  
|VALUETYPE|  
|---------------|  
|1 (Missing)|  
|3 (Continuous)|  
|7 (Koeffizient)|  
|8 (Score Gain)|  
|9 (Statistik)|  
|11 (Intercept)|  
  
 NODE_SUPPORT  
 Die Anzahl der Fälle, die diesen Knoten unterstützen.  
  
 **Stammknoten:** 0  
  
 **Regressionsknoten:** Anzahl der Trainingsfälle.  
  
 MSOLAP_MODEL_COLUMN  
 Name des vorhersagbaren Attributs.  
  
 MSOLAP_NODE_SCORE  
 Entspricht NODE_PROBABILITY  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Eine zu Anzeigezwecken verwendete Beschriftung.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie ein Modell mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus erstellen, generiert das Data Mining-Modul eine besondere Instanz eines Entscheidungsstrukturmodells und liefert Parameter, die die Struktur darauf beschränkt, alle Trainingsdaten in einem einzelnen Knoten zu enthalten. Alle kontinuierlichen Eingaben werden als potenzielle Regressoren gekennzeichnet und als solche bewertet, aber nur diejenigen Regressoren, die den Daten entsprechen, werden als Regressoren in das endgültige Modell übernommen. Die Analyse erzeugt entweder eine einzelne Regressionsformel für jeden Regressor oder keine Regressionsformel.  
  
 Sie können die vollständige Regressionsformel unter **Mininglegende**einsehen, indem Sie auf den Knoten **(Alle)** im [Microsoft Struktur-Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)klicken.  
  
 Wenn Sie ein Entscheidungsstrukturmodell erstellen, das ein kontinuierliches, vorhersagbares Attribut enthält, verfügt die Struktur zuweilen über Regressionsknoten, die die Eigenschaften von Regressionsstrukturknoten aufweisen.  
  
##  <a name="NodeDist_Regression"></a> Knotenverteilung für kontinuierliche Attribute  
 Die meisten der wichtigen Informationen in einem Regressionsknoten sind in der NODE_DISTRIBUTION-Tabelle enthalten. Im folgenden Beispiel wird das Layout der NODE_DISTRIBUTION-Tabelle veranschaulicht. In diesem Beispiel wurde die Targeted Mailing-Miningstruktur verwendet, um ein lineares Regressionsmodell zu erstellen, das basierend auf dem Alter das Kundeneinkommen vorhersagt. Das Modell dient lediglich Anschauungszwecken, da es mithilfe der bestehenden [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Beispieldaten und -Miningstruktur leicht erstellt werden kann.  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Yearly Income|Nicht vorhanden|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Age|471.687717702463|0|0|126.969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 Die NODE_DISTRIBUTION-Tabelle enthält mehrere Zeilen, die jeweils durch eine Variable gruppiert sind. Die ersten zwei Zeilen sind immer die Werttypen 1 und 3 und beschreiben das Zielattribut. Die folgenden Zeilen stellen Details über die Formel für einen besonderen *Regressor*bereit. Ein Regressor ist eine Eingangsvariable, die eine lineare Beziehung mit der Ausgabevariablen hat. Es sind mehrere Regressoren möglich und jeder Regressor verfügt über eine separate Zeile für den Koeffizienten (VALUETYPE = 7), den Ergebnisgewinn (VALUETYPE = 8) und die Statistik (VALUETYPE = 9). Schließlich verfügt die Tabelle über eine Zeile, die das konstante Glied der Gleichung (VALUETYPE = 11) enthält.  
  
### <a name="elements-of-the-regression-formula"></a>Elemente der Regressionsformel  
 Die geschachtelte NODE_DISTRIBUTION-Tabelle enthält jedes Element der Regressionsformel in einer separaten Zeile. Die ersten beiden Zeilen von Daten in den Beispielergebnissen enthalten Informationen über das vorhersagbare Attribut **Yearly Income**, das die unabhängige Variable modelliert. In der Spalte SUPPORT wird die Anzahl der Fälle gezeigt, die die beiden Status dieses Attributs unterstützen: entweder stand ein Wert **Yearly Income** zur Verfügung oder der Wert **Yearly Income** fehlte.  
  
 Die Spalte VARIANCE gibt Aufschluss über die berechnete Varianz des vorhersagbaren Attributs. *Varianz* ist ein Maß dafür, wie zerstreut die Werte in einem Beispiel angesichts einer erwarteten Verteilung sind. Die Varianz wird berechnet, indem der durchschnittliche Wert der quadratischen Abweichung vom Mittelwert genommen wird. Die Quadratwurzel der Varianz wird auch als Standardabweichung bekannt. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt die Standardabweichung nicht bereit; Sie können diese jedoch leicht berechnen.  
  
 Für jeden Regressor werden drei Zeilen ausgegeben. Sie enthalten den Koeffizienten, den Ergebnisgewinn und die Regressorstatistik.  
  
 Schließlich enthält die Tabelle eine Zeile, die das konstante Glied der Gleichung bereitstellt.  
  
#### <a name="coefficient"></a>Koeffizient  
 Für jeden Regressor wird ein Koeffizient (VALUETYPE = 7) berechnet. Der Koeffizient selbst erscheint in der Spalte ATTRIBUTE_VALUE, während die Spalte VARIANCE die Varianz für den Koeffizienten angibt. Die Koeffizienten werden berechnet, um Linearität zu maximieren.  
  
#### <a name="score-gain"></a>Ergebnisgewinn  
 Der Ergebnisgewinn (VALUETYPE = 8) für jeden Regressor stellt den Interessantheitsgrad des Attributs dar. Sie können diesen Wert verwenden, um die Nützlichkeit von mehreren Regressoren einzuschätzen.  
  
#### <a name="statistics"></a>Statistik  
 Die Regressorstatistik (VALUETYPE = 9) ist der Mittelwert für das Attribut für Fälle, die über einen Wert verfügen. Die Spalte ATTRIBUTE_VALUE enthält den Mittelwert selbst, während die Spalte VARIANCE die Summe der Abweichungen vom Mittelwert enthält.  
  
#### <a name="intercept"></a>Konstantes Glied  
 In der Regel gibt das *konstante Glied* (VALUETYPE = 11) oder das *Residuum* in einer Regressionsgleichung den Wert des vorhersagbaren Attributs an dem Punkt an, an dem das Eingabeattribut 0 ist. In vielen Fällen geschieht dies nicht und könnte zu nicht intuitiven Ergebnissen führen.  
  
 Beispielsweise ist es bei einem Modell, das das Einkommen basierend auf dem Alter vorhersagt, nicht nützlich, das Einkommen bei einem Alter von 0 Jahren anzugeben. In realen Situationen ist es in der Regel nützlicher, das Verhalten in Bezug auf einen Durchschnittswert zu erfahren. Daher ändert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das kontante Glied so, dass jeder Regressor in Beziehung zum Mittelwert ausgedrückt wird.  
  
 Diese Anpassung ist im Miningmodellinhalt schwer ersichtlich. Sie wird erst deutlich, wenn man die vollständige Gleichung in der **Mininglegende** des **Microsoft Struktur-Viewer**einsieht. Die Regressionsformel wird weg vom Punkt 0 zu dem Punkt verlagert, der den Mittelwert darstellt. Dies stellt eine Sicht dar, die angesichts der aktuellen Daten intuitiver ist.  
  
 Daher gibt das konstante Glied (VALUETYPE = 11) für die Regressionsformel bei einem Durchschnittsalter von 45 ein durchschnittliches Einkommen an.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodellinhalt & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Microsoft Linear Regression-Algorithmus](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [Technische Referenz zu Microsoft Linear Regression-Algorithmus](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [Beispiele für lineare Regressionsmodellabfragen](../../analysis-services/data-mining/linear-regression-model-query-examples.md)  
  
  
