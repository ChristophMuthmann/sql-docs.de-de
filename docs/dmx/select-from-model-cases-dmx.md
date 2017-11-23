---
title: "SELECT FROM &lt;Modell&gt;. FÄLLE (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
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
ms.topic: language-reference
f1_keywords:
- SELECT
- CASES
- FROM
dev_langs: DMX
helpviewer_keywords:
- SELECT FROM <model>.CASES statement
- drillthrough [DMX]
ms.assetid: d58acb47-aaa6-40b7-b8c4-6a6700fbc1dd
caps.latest.revision: "55"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1a02b3f56bd56fd7b86bbf3a998b7fdfd7316e9d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM &lt;Modell&gt;. FÄLLE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Unterstützt Drillthrough und gibt die Fälle zurück, mit denen das Modell trainiert wurde. Sie können auch Strukturspalten zurückgeben, die nicht im Modell enthalten sind, wenn Drillthrough sowohl für die Miningstruktur als auch für das Miningmodell aktiviert wurde und wenn Sie über die entsprechenden Berechtigungen verfügen.  
  
 Wenn Drillthrough nicht für das Miningmodell aktiviert ist, erzeugt diese Anweisung einen Fehler.  
  
> [!NOTE]  
>  In Data Mining-Erweiterungen (DMX) können Sie Drillthrough nur beim Erstellen des Modells aktivieren. Mit [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] können Sie Drillthrough zu einem vorhandenen Modell hinzufügen. Das Modell muss jedoch erneut verarbeitet werden, bevor Sie die Fälle anzeigen oder abfragen können.  
  
 Weitere Informationen zur drillthroughaktivierung finden Sie unter [CREATE MINING MODEL &#40; DMX &#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md), und [ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumente  
 *n*  
 Optional. Eine ganze Zahl, die angibt, wie viele Zeilen zurückgegeben werden sollen.  
  
 *Liste der Ausdrücke*  
 Eine Liste von Ausdrücken, die durch Trennzeichen voneinander getrennt sind. Ein Ausdruck kann u. a. Spaltenbezeichner, benutzerdefinierte Funktionen und VBA-Funktionen einschließen.  
  
 Um eine Strukturspalte einzuschließen, die nicht im Miningmodell enthalten ist, verwenden Sie die Funktion `StructureColumn('<structure column name>')`.  
  
 *model*  
 Ein Modellbezeichner.  
  
 *Bedingungsausdruck*  
 Eine Bedingung, die die Werte einschränkt, die für die Spaltenliste zurückgegeben werden.  
  
 *expression*  
 Optional. Ein Ausdruck, der einen Skalarwert zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie Drillthrough sowohl für das Miningmodell als auch für die Miningstruktur aktivieren, können Benutzer, die Mitglied einer Rolle mit Drillthroughberechtigungen für das Miningmodell und die Miningstruktur sind, auf Spalten in der Miningstruktur zugreifen, die nicht Teil des Miningmodells sind. Aus diesem Grund zum Schutz sensibler oder persönlicher Informationen sollten, erstellen Sie die Datenquellensicht aus, um persönliche Informationen verborgen sind, und gewähren **AllowDrillthrough** -Berechtigung für eine Miningstruktur nur bei Bedarf.  
  
 Die [Lag &#40; DMX &#41;](../dmx/lag-dmx.md) Funktion kann zum zurückgeben, oder Filtern die zeitverzögerung zwischen jedem Fall und der Anfangszeit mit zeitreihenmodellen verwendet werden.  
  
 Mithilfe der [IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md) -Funktion in der **, in denen** -Klausel nur Fälle zurückgegeben, die dem Knoten zugeordnet sind, durch die NODE_UNIQUE_NAME-Spalte des Schemarowsets angegeben ist.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele beruhen auf der Miningstruktur Targeted Mailing, die basierend auf den [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]Datenbank und den zugeordneten Miningmodellen. Weitere Informationen finden Sie unter [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>Beispiel 1: Drillthrough zu Modellfällen und Strukturspalten  
 Im folgenden Beispiel werden die Spalten für alle Fälle zurückgegeben, die zum Testen des Target Mailing-Modells verwendet wurden. Wenn die Miningstruktur, auf der das Modell aufbaut, kein Zurückhaltungstestdataset enthält, werden bei dieser Abfrage 0 Fälle zurückgegeben. Sie können die Ausdrucksliste dazu verwenden, nur die benötigten Spalten zurückzugeben.  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>Beispiel 2: Drillthrough zu Trainingsfällen in einem bestimmten Knoten  
 Im folgenden Beispiel werden nur jene Fälle zurückgegeben, die verwendet wurden, um Cluster 2 zu trainieren. Der Knoten für Cluster 2 verfügt über den Wert "002" für die Spalte NODE_UNIQUE_NAME. Das Beispiel gibt außerdem eine Strukturspalte zurück, [Customer Key], die nicht Teil des Miningmodells war, und stellt den Alias `CustomerID` für die Spalte zur Verfügung. Beachten Sie, dass der Name der Strukturspalte als Zeichenfolgenwert übergeben wird und daher in Anführungszeichen und nicht in Klammern gesetzt werden muss.  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 Um eine Strukturspalte zurückzugeben, müssen Drillthroughberechtigungen sowohl im Miningmodell als auch in der Miningstruktur aktiviert sein.  
  
> [!NOTE]  
>  Nicht alle Miningmodelltypen unterstützen Drillthrough. Weitere Informationen zu den Modellen, die Drillthrough unterstützen, finden Sie unter [Drillthroughabfragen &#40; Data Mining &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
