---
title: SELECT INTO (DMX) | Microsoft Docs
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
- SELECT_INTO
- SELECT INTO
dev_langs:
- DMX
helpviewer_keywords:
- mining models [Analysis Services], copying
- SELECT INTO statement
- mining models [Analysis Services], creating
- copying mining models
ms.assetid: 31ab9b4c-e20d-41ee-886f-6665c22c6ad5
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: db4e68e8051e1104ce9ed7ad42d8ac9f86a98274
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Erstellt ein neues Miningmodell, das auf der Miningstruktur eines vorhandenen Miningmodells basiert. Die **SELECT INTO** -Anweisung erstellt das neue Miningmodell durch Kopieren von Schema und andere Informationen, die nicht zum konkreten Algorithmus spezifisch ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>Argumente  
 *Neues Modell*  
 Ein eindeutiger Name für das neue Modell, das erstellt wird.  
  
 *Algorithmus*  
 Der vom Anbieter definierte Name eines Data Mining-Algorithmus.  
  
 *Parameterliste*  
 Optional. Eine durch Trennzeichen getrennte Liste mit anbieterdefinierten Parametern für den Algorithmus.  
  
 *expression*  
 Ein Ausdruck, der auf den Trainingsdaten eine gültige Filterbedingung ergibt. Weitere Informationen zu Ausdrücken, die als Filter verwendet werden können, finden Sie unter [Filter für Miningmodelle &#40; Analysis Services – Datamining &#41; ](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 *vorhandenes Modell*  
 Der Name des vorhandenen Modells, das kopiert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Wenn das vorhandene Modell trainiert ist, wird das neue Modell automatisch verarbeitet, wenn diese Anweisung ausgeführt wird. Anderenfalls bleibt das neue Modell unverarbeitet.  
  
 Die **SELECT INTO** Anweisung funktioniert nur, wenn die Struktur des vorhandenen Modells mit dem Algorithmus des neuen Modells kompatibel ist. Daher ist diese Anweisung sehr zweckmäßig, um Modelle, die auf dem gleichen Algorithmus basieren, schnell zu erstellen und zu testen. Wenn Sie den Algorithmustyp ändern, muss der neue Algorithmus den Datentyp einer jeden Spalte unterstützen, die sich im vorhandenen Modell befindet, andernfalls tritt bei der Verarbeitung des Modells möglicherweise ein Fehler auf.  
  
 Die **WITH DRILLTHROUGH** -Klausel aktiviert Drillthrough für das neue Miningmodell. Drillthrough kann nur aktiviert werden, wenn das Modell erstellt wird.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>Beispiel 1: Ändern der Parameter des Modells  
 Das folgende Beispiel erstellt ein neues Miningmodell, basierend auf einem vorhandenen Miningmodell `TM_Clustering`, die Sie erstellen, in der [Data Mining-Grundlagen](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). In dem neuen Modell wird der CLUSTER_COUNT-Parameter geändert, sodass das neue Modell maximal fünf Cluster enthält. Demgegenüber verwendet das vorhandene Modell den Standardwert 10.  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>Beispiel 2: Hinzufügen eines Filters zu dem Modell  
 Im folgenden Beispiel wird ein neues Miningmodell auf der Grundlage eines vorhandenen Miningmodells erstellt und dem Modell ein Filter hinzugefügt. Der Filter beschränkt die Trainingsdaten auf die Kunden, die in einer bestimmten Region wohnen.  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  Filter, die auf die Falltabelle angewendet werden, können mithilfe der SELECT INTO-Anweisung geändert werden, wie in diesem Beispiel erläutert wird. Wenn das ursprüngliche Modell jedoch einen Filter für eine geschachtelte Tabelle enthält, kann dieser Filter nicht mithilfe dieser Syntax geändert oder entfernt werden, er wird stattdessen unverändert aus dem ursprünglichen Modell kopiert. Um ein Modell mit einem anderen Filter für eine geschachtelte Tabelle zu erstellen, verwenden Sie stattdessen die ALTER STRTUCTURE...ADD MODEL-Syntax.  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

