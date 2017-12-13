---
title: Modellierungsflags (Datamining) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- attributes [data mining]
- data types [data mining]
- REGRESSOR flag
- MODEL_EXISTENCE_ONLY flag
- REGRESSOR column
- columns [data mining], modeling flags
- NOT NULL modeling flag
- modeling flags [data mining]
- null values [Analysis Services]
- MODEL_EXISTENCE_ONLY column
- coding [Data Mining]
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
caps.latest.revision: "48"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fbe2029742ba4df3c390820effa565055159f7dd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="modeling-flags-data-mining"></a>Modellierungsflags (Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können Modellierungsflags in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für Datamining-Algorithmus zusätzliche Informationen zu den Daten bereitstellen, die in einer Falltabelle definiert ist. Der Algorithmus kann diese Informationen verwenden, um ein genaueres Data Mining-Modell zu erstellen.  
  
 Einige Modellierungsflags werden auf der Ebene der Miningstruktur definiert, während andere auf der Ebene der Miningmodellspalte definiert werden. Beispielsweise wird das **NOT NULL** -Modellierungsflag für Miningstrukturspalten verwendet. Sie können zusätzliche Modellierungsflags für die Miningmodellspalten definieren, abhängig vom Algorithmus, den Sie zur Erstellung des Modells verwenden.  
  
> [!NOTE]  
>  Zusätzlich zu den von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]vordefinierten Modellierungsflags können Plug-Ins eines Drittanbieters über eigene Modellierungsflags verfügen.  
  
## <a name="list-of-modeling-flags"></a>Liste der Modellierungsflags  
 In der folgenden Liste werden die Modellierungsflags beschrieben, die in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]unterstützt werden. Weitere Informationen zu den Modellierungsflags, die von bestimmten Algorithmen unterstützt werden, finden Sie unter dem Thema in der technischen Referenz für den Algorithmus, der zur Erstellung des Modells verwendet wurde.  
  
 **NOT NULL**  
 Gibt an, dass die Werte für die Attributspalte auf keinen Fall einen NULL-Wert enthalten dürfen. Es führt zu einem Fehler, wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] während des Modelltrainings einen NULL-Wert für diese Attributspalte findet.  
  
 **MODEL_EXISTENCE_ONLY**  
 Dies bedeutet, dass die Spalte zwei mögliche Statuswerte haben kann: **Missing** und **Existing**. Der Wert **NULL**wird wie der Wert Missing behandelt. Das MODEL_EXISTENCE_ONLY-Flag wird für das vorhersagbare Attribut übernommen und wird von den meisten Algorithmen unterstützt.  
  
 Tatsächlich wird durch Festlegen des MODEL_EXISTENCE_ONLY-Flags auf **TRUE** die Darstellung der Werte so geändert, dass es nur zwei Status gibt: **Missing** und **Existing**. Alle nicht fehlenden Status werden in einem einzelnen **Existing** -Wert kombiniert.  
  
 Dieses Modellierungsflag wird in der Regel in Attributen verwendet, bei denen der **NULL** -Status eine implizite Bedeutung hat und der explizite Wert des **NOT NULL** -Status nicht so wichtig ist wie die Tatsache, dass die Spalte überhaupt einen Wert enthält. Beispielsweise kann die Spalte [DateContractSigned] den Wert **NULL** annehmen, wenn ein Vertrag nie unterschrieben wurde, und den Wert **NOT NULL** , wenn der Vertrag unterschrieben wurde. Wenn das Modell vorhersagen soll, ob ein Vertrag unterschrieben wird, können Sie daher das MODEL_EXISTENCE_ONLY-Flag einsetzen, um den genauen Datumswert in den Fällen mit **NOT NULL** zu ignorieren und nur zwischen den Fällen zu unterscheiden, in denen ein Vertrag **Missing** oder **Existing**lautet.  
  
> [!NOTE]  
>  Missing ist ein spezieller vom Algorithmus verwendeter Statuswert, der nicht mit dem Textwert "Missing" bzw. "Fehlend" einer Spalte gleichbedeutend ist. Weitere Informationen finden Sie unter [Fehlende Werte &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)vordefinierten Modellierungsflags können Plug-Ins eines Drittanbieters über eigene Modellierungsflags verfügen.  
  
 **REGRESSOR**  
 Gibt an, dass die Spalte ein Kandidat für die Verwendung als Regressor während der Verarbeitung ist. Dieses Flag wird in einer Miningmodellspalte definiert und kann nur auf Spalten angewendet werden, die einen fortlaufenden numerischen Datentyp aufweisen. Weitere Informationen zur Verwendung dieses Flags finden Sie im Abschnitt in diesem Thema: [Verwendungszwecke für das REGRESSOR-Modellierungsflag](#bkmk_UseRegressors).  
  
## <a name="viewing-and-changing-modeling-flags"></a>Anzeigen und Ändern von Modellierungsflags  
 Sie können die Modellierungsflags, die einer Miningstrukturspalte oder Modellspalte im Data Mining-Designer zugeordnet sind, betrachten, indem Sie die Eigenschaften der Struktur oder des Modells anzeigen.  
  
 Um zu bestimmen, welche Modellierungsflags für die aktuelle Miningstruktur übernommen wurden, können Sie eine Abfrage für das Data Mining-Schemarowset erstellen, das die Modellierungsflags ausschließlich für die Strukturspalten zurückgibt, indem eine Abfrage wie die Folgende verwendet wird:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 Sie können die in einem Modell verwendeten Modellierungsflags hinzufügen oder ändern, indem Sie den Data Mining-Designer verwenden und die Eigenschaften der zugeordneten Spalten bearbeiten. Für solche Änderungen ist es erforderlich, dass die Struktur oder das Modell erneut verarbeitet wird.  
  
 Sie können Modellierungsflags in einer neuen Miningstruktur oder einem Miningmodell mithilfe von DMX oder AMO- oder XMLA-Skripts angeben. Die in einem vorhandenen Miningmodell und einer Struktur mit DMX verwendeten Modellierungsflags können jedoch nicht geändert werden. Sie müssen unter Verwendung der `ALTER MINING STRUCTURE….ADD MINING MODEL`-Syntax ein neues Miningmodell erstellen.  
  
##  <a name="bkmk_UseRegressors"></a> Verwendungszwecke für das REGRESSOR-Modellierungsflag  
 Wenn Sie das REGRESSOR-Modellierungsflag für eine Spalte festlegen, zeigen Sie dem Algorithmus damit an, dass die Spalte potenzielle Regressoren enthält. Die tatsächlich im Modell verwendeten Regressoren werden vom Algorithmus bestimmt. Ein potenzieller Regressor kann verworfen werden, wenn er das vorhersagbare Attribut nicht modelliert.  
  
 Wenn Sie mit dem Data Mining-Assistenten ein Modell erstellen, werden alle kontinuierlichen Eingabespalten als potenzielle Regressoren gekennzeichnet. Daher kann eine Spalte im Modell auch dann als Regressor verwendet werden, wenn für diese Spalte nicht explizit das REGRESSOR-Flag festgelegt wurde.  
  
 Sie können ermitteln, welche Regressoren im verarbeiteten Modell tatsächlich verwendet wurden, indem Sie, wie im folgenden Beispiel gezeigt, eine Abfrage auf das Schemarowset des Miningmodells ausführen:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **Hinweis** Wenn Sie ein Miningmodell verändern und den Inhaltstyp einer Spalte von kontinuierlich in diskret ändern, müssen Sie das Flag für die Miningspalte von Hand ändern und das Modell dann erneut verarbeiten.  
  
### <a name="regressors-in-linear-regression-models"></a>Regressoren in linearen Regressionsmodellen  
 Lineare Regressionsmodelle basieren auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus. Auch wenn Sie den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus nicht verwenden, kann jedes Entscheidungsstrukturmodell eine Struktur oder Knoten enthalten, die eine Regression für ein kontinuierliches Attribut darstellt bzw. darstellen.  
  
 Sie müssen in diesen Modellen nicht angeben, dass eine kontinuierliche Spalte einen Regressor darstellt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus unterteilt das Dataset selbst dann in Bereiche mit sinnvollen Mustern, wenn Sie das REGRESSOR-Flag nicht für die Spalte festlegen. Wenn das Modellierungsflag festgelegt wurde, versucht der Algorithmus im Unterschied dazu Regressionsgleichungen der folgenden Form zu finden, um die Muster den Knoten der Struktur zuzuordnen.  
  
 a*C1 + b\*C2 + ...  
  
 Dann wird die Summe der Restwerte berechnet, und wenn die Abweichung zu groß ist, wird die Struktur unterteilt.  
  
 Wenn Sie beispielsweise das Kaufverhalten von Kunden mithilfe des Attributs **Income** vorhersagen und das Modellierungsflag REGRESSOR für die Spalte festlegen, versucht der Algorithmus zuerst, die Werte der Spalte **Income** mithilfe einer Standardregressionsformel zuzuordnen. Ist die Abweichung zu groß, dann wird die Regressionsformel ignoriert und die Struktur nach einem anderen Attribut unterteilt. Der Decision Tree-Algorithmus versucht nach der Unterteilung, jedem der Zweige einen Regressor für Einkommen zuzuordnen.  
  
 Sie können durch Einsatz des FORCE_REGRESSOR-Parameters gewährleisten, dass der Algorithmus einen bestimmten Regressor verwendet. Dieser Parameter kann mit dem Decision Trees-Algorithmus und dem Linear Regression-Algorithmus verwendet werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Verwenden Sie die folgenden Links, um weitere Informationen zum Verwenden von Modellierungsflags zu erhalten.  
  
|Task|Thema|  
|----------|-----------|  
|Bearbeiten von Modellierungsflags mit dem Data Mining-Designer|[Anzeigen oder Ändern von Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Angeben eines Tipps für den Algorithmus, um wahrscheinliche Regressoren zu empfehlen|[Bestimmen einer in einem Modell als Regressor zu verwendenden Spalte](../../analysis-services/data-mining/specify-a-column-to-use-as-regressor-in-a-model.md)|  
|Siehe die von bestimmten Algorithmen (im Abschnitt "Modellierungsflags" für jedes Algorithmusreferenzthema) unterstützten Modellierungsflags|[Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)|  
|Weitere Informationen zu Miningstrukturspalten und den Eigenschaften, die Sie festlegen können|[Miningstrukturspalten](../../analysis-services/data-mining/mining-structure-columns.md)|  
|Weitere Informationen zu Miningmodellspalten und Modellierungsflags, die für die Modellebene übernommen werden können|[Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md)|  
|Siehe Syntax zum Arbeiten mit Modellierungsflags in DMX-Anweisungen|[Modellierungsflags &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|Verstehen von fehlenden Werten und wie mit diesen gearbeitet wird|[Fehlende Werte &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)|  
|Weitere Informationen zum Verwalten von Modellen und Strukturen sowie Festlegen von Verwendungseigenschaften|[Verschieben von Data Mining-Objekten](../../analysis-services/data-mining/moving-data-mining-objects.md)|  
  
  
