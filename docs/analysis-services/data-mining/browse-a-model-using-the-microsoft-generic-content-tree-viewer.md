---
title: Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 540228c694ee222d9c854b32b3c0939adcaeadb4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für generische Miningmodellinhalte enthält ausführliche Informationen über die vom Miningalgorithmus erfassten Muster und bietet zudem Zugang zu verschiedenen Statistiken, die während des Analysevorgangs generiert werden. Die Menge und Art der Informationen hängen von dem verwendeten Algorithmus ab und können folgende Kategorien umfassen:  
  
-   Segmente der Daten und ihre Eigenschaften.  
  
-   Beschreibende Statistik zu jeder Gruppe oder zum gesamten Datensatz.  
  
-   Die Anzahl von Verzweigungen oder untergeordnete Knoten in einer Struktur.  
  
-   Berechnungen, z. B. Varianz und Mitte, für einen Cluster oder einen Datensatz.  
  
 Durch Anzeigen dieser Informationen können Sie die Ergebnisse der Analyse besser verstehen. Sie können auch Möglichkeiten identifizieren, Ihr Modell zu optimieren und anschließend erneut mit Daten zu trainieren. Oder Sie können sich dazu entschließen, Ihr Modell mit einem anderen Algorithmus erneut zu trainieren.  
  
## <a name="viewing-mining-model-content"></a>Anzeigen von Miningmodellinhalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Viewer zeigt die im *Schemarowset für den Inhalt* des Miningmodells enthaltenen Spalten, Regeln, Eigenschaften, Attribute, Knoten sowie andere Inhalte an. Das Schemarowset für den Inhalt ist ein allgemeines Framework zum Darstellen detaillierter Informationen über den Inhalt eines Data Mining-Modells.  
  
 Diese ausführlichen Informationen sind in einer HTML-Tabelle enthalten, in der die Muster, Cluster oder Strukturen im Modell als Knoten dargestellt werden. Sie können auf jeden Knoten klicken und ihn erweitern, um weitere Details anzuzeigen, z.B. die Formeln oder die Anzahl der unterschiedlichen Werte für ein numerisches Attribut. Sie können auch die Beziehungen zwischen unter- und übergeordneten Elementen unter den Knoten untersuchen.  
  
 Weitere Informationen zur allgemeinen Bedeutung der in den Miningmodellinhalten verwendeten Begriffe finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md). Das Thema enthält außerdem Links zu Informationen über Miningmodellinhalte für bestimmte Modelltypen. Jeder Miningmodelltyp enthält Informationen, die eng mit dem Algorithmus und den in den Daten gefundenen Mustern zusammenhängen. Daher wird empfohlen, die technische Referenz für den jeweiligen Modelltyp zu lesen, um jeden Modelltyp genau zu verstehen.  
  
## <a name="querying-mining-model-content"></a>Abfragen von Miningmodellinhalten  
 Die im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer enthaltenen Informationen können auch durch Abfragen des Miningmodells abgerufen werden. Abfragen für Miningmodellinhalt können Sie mithilfe von DMX-Anweisungen (Data Mining-Erweiterungen) erstellen. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]können Sie beispielsweise durch das Ausführen der folgenden DMX-Anweisung eine Inhaltsabfrage ausführen:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Weitere Informationen finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Generic Content Tree Viewer & #40; Datamining & #41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Datamining-Algorithmen & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
