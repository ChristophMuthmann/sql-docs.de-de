---
title: "Data Mining-Abfragen, Tasks und Anweisungen für | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 599ad86e236619b5bfa3798a94e3cc0044746db3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-query-tasks-and-how-tos"></a>Data Mining-Abfragetasks und Anweisungen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die Fähigkeit zum Erstellen von Abfragen ist wichtig, wenn Sie zu der die Datamining-Modelle verwenden. Dieser Abschnitt enthält Links zu Beispielen, die die Erstellung von Abfragen für ein Data Mining-Modell mithilfe der Tools in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]veranschaulichen. Weitere Informationen zu Data Mining-Abfragen oder den unterschiedlichen Abfragetypen, die erstellt werden können, finden Sie unter [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="creating-queries-with-prediction-query-builder"></a>Erstellen von Abfragen mit dem Generator für Vorhersageabfragen  
 Der Generator für Vorhersageabfragen steht sowohl in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] als auch in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] als Methode der grafischen Erstellung von Abfragen für Data Mining-Modelle zur Verfügung. In den folgenden Themen wird erläutert, wie Sie ein Modell auswählen, eine Datenquelle angeben, die Vorhersagen anpassen und die Ausgabe speichern können.  
  
-   [Erstellen von Vorhersageabfragen mithilfe des Generators für Vorhersageabfragen](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [Erstellen einer SINGLETON-Abfrage im Data Mining-Designer](../../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [Erstellen von Vorhersageabfragen mithilfe des Generators für Vorhersageabfragen](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [Anzeigen und Speichern der Ergebnisse einer Vorhersageabfrage](../../analysis-services/data-mining/view-and-save-the-results-of-a-prediction-query.md)  
  
-   [Manuelles Bearbeiten einer Vorhersageabfrage](../../analysis-services/data-mining/manually-edit-a-prediction-query.md)  
  
-   [Anwenden von Vorhersagefunktionen auf ein Modell](../../analysis-services/data-mining/apply-prediction-functions-to-a-model.md)  
  
-   [Auswählen und Zuordnen von Eingabedaten für eine Vorhersageabfrage](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>Verwenden von Tools für Data Mining-Abfragen  
 Neben der Verwendung des Generators für Vorhersagenabfragen besteht außerdem die Möglichkeit, eine Abfrage mit DMX oder XMLA direkt in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einzugeben. Sie können auch programmgesteuert Vorhersageabfragen erstellen und sie an einen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server senden. Die folgenden Themen enthalten weitere Informationen zur Erstellung und Verwendung von Vorhersageabfragen außerhalb des Vorhersageabfragen-Generators.  
  
 [Erstellen einer Singleton-Vorhersageabfrage aus einer Vorlage](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
 Beschreibt, wie mit den Tools in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Vorhersageabfrage erstellt und ausgeführt wird.  
  
 [Erstellen einer SINGLETON-Vorhersageabfrage aus einer Vorlage](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
 Beschreibt, wie mit den in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügbaren Vorlagen einer Vorhersageabfrage Parameter hinzugefügt werden.  
  
 [Ändern des Timeoutwerts für Data Mining-Abfragen](../../analysis-services/data-mining/change-the-time-out-value-for-data-mining-queries.md)  
 Beschreibt, wie Eigenschaften auf dem Server, der das auf Data Mining-Abfragen bezogene Verhalten steuert, festgelegt werden.  
  
 [Erstellen einer Miningmodell-Inhaltsabfrage](../../analysis-services/data-mining/create-a-content-query-on-a-mining-model.md)  
 Beschreibt die Erstellung von Abfragen, bei denen unter Verwendung der Data Mining-Schemarowsets ausführliche Informationen zurückgegeben werden, die im Miningmodell gespeichert sind.  
  
 [Erstellen einer Data Mining-Abfrage mit XMLA](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)  
 Beschreibt, wie eine Abfrage für einen Miningmodellinhalt mit den XMLA-Vorlagen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Abfragen- und Ausdruckssprachreferenz &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527)   
 [Data Mining-gespeicherte Prozeduren &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)  
  
  
