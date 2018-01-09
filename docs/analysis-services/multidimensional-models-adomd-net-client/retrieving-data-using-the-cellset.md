---
title: Abrufen von Daten mittels CellSet | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- CellSet object
- retrieving data
- data retrieval [ADOMD.NET], CellSet object
ms.assetid: 77e4ee58-882d-4012-91a3-0565f18a4882
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e1552ce0646c48465aac824f40d9f42f8aa4215d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="retrieving-data-using-the-cellset"></a>Abrufen von Daten mittels Cellset
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Beim Abrufen von analytischen Daten, die <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> -Objekt stellt die meiste Interaktivität und Flexibilität bereit. Das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt ist ein im Arbeitsspeicher befindlicher Cache für hierarchische Daten und Metadaten, der die ursprüngliche Dimensionalität der Daten beibehält. Das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt kann darüber hinaus in einen Online- oder Offlinezustand traversiert werden. Aufgrund dieser Offline-Fähigkeit kann das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt verwendet werden, um Daten und Metadaten in beliebiger Reihenfolge einzusehen, und es stellt das umfangreichste Objektmodell für die Datenabfrage bereit. Diese Offline-Fähigkeit führt dazu, dass das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt den größten Verwaltungsaufwand erfordert und von allen ADOMD.NET-Objektmodellen zur Datenabfrage das langsamste ist.  
  
## <a name="retrieving-data-in-a-connected-state"></a>Abrufen von Daten im Onlinezustand  
 Um das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt für das Abrufen von Daten zu verwenden, führen Sie die folgenden Schritte durch:  
  
1.  **Erstellen Sie eine neue Instanz des Objekts.**  
  
     Um eine neue Instanz des <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekts zu generieren, rufen Sie die Methode <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> oder die Methode <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekts auf.  
  
2.  **Identifizieren Sie die Metadaten.**  
  
     Neben dem Abruf von Daten ruft ADOMD.NET auch Metadaten für das Cellset ab. Sobald der Befehl die Abfrage ausgeführt und einen <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> zurückgegeben hat, können Sie die Metadaten über diverse Objekte abrufen. Diese Metadaten werden benötigt, damit Clientanwendungen Cellsetdaten anzeigen und mit diesen interagieren können. Beispielsweise bieten viele Clientanwendungen Funktionen für ein Drilldown oder eine hierarchische Anzeige der untergeordneten Positionen einer angegebenen Position im Cellset.  
  
     In ADOMD.NET stellen die Eigenschaften <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> und <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> des <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekts die Metadaten der Abfrage und der Slicerachsen im zurückgegebenen Cellset dar. Beide Eigenschaften geben Verweise auf <xref:Microsoft.AnalysisServices.AdomdClient.Axis>-Objekte zurück, die wiederum die Positionen enthalten, die auf jeder Achse dargestellt sind.  
  
     Jedes <xref:Microsoft.AnalysisServices.AdomdClient.Axis>-Objekt enthält eine Auflistung von <xref:Microsoft.AnalysisServices.AdomdClient.Position>-Objekten, die die Menge der Tupel darstellen, die für diese Achse verfügbar sind. Jedes <xref:Microsoft.AnalysisServices.AdomdClient.Position>-Objekt stellt ein einzelnes Tupel dar, das ein oder mehr Elemente enthält, die durch eine Auflistung von <xref:Microsoft.AnalysisServices.AdomdClient.Member>-Objekten dargestellt werden.  
  
3.  **Abrufen von Daten aus der cellsetauflistung ab.**  
  
     Neben dem Abruf von Metadaten ruft ADOMD.NET auch Daten für das Cellset ab. Sobald der Befehl die Abfrage ausgeführt und einen <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> zurückgegeben hat, können Sie die Daten über die <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A>-Auflistung von <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> abrufen. Diese Auflistung enthält die Werte, die für die Schnittmenge aller Achsen in der Abfrage berechnet werden. Deshalb gibt es mehrere Indexer für den Zugriff auf jede Schnittmenge oder Zelle. Eine Liste der Indexer finden Sie unter <xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>.  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>Beispiel für das Abrufen von Daten im Onlinezustand  
 Das folgende Beispiel stellt eine Verbindung zum lokalen Server her und führt dann einen Befehl auf der Verbindung aus. Das Beispiel analysiert die Ergebnisse mithilfe der **CellSet** Objektmodell: die Beschriftungen (Metadaten) für die Spalten aus der ersten Achse abgerufen, und die Beschriftungen (Metadaten) für jede Zeile aus der zweiten Achse abgerufen und die überschneidenden Daten wird abgerufen, wobei die <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> Auflistung.  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_1.cs)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>Abrufen von Daten im Offlinezustand  
 Durch das Laden von XML, das in einer vorherigen Abfrage zurückgegeben wurde, können Sie das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt verwenden, um eine umfangreiche Methode für das Durchsuchen analytischer Daten bereitzustellen, ohne dass eine aktive Verbindung erforderlich ist.  
  
> [!NOTE]  
>  Nicht alle Eigenschaften der Objekte, die über das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekt verfügbar sind, sind auch im Offlinezustand verfügbar. Weitere Informationen finden Sie unter <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>.  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>Beispiel für das Abrufen von Daten im Offlinezustand  
 Das folgende Beispiel ähnelt dem zuvor in diesem Thema behandelten Metadaten- und Datenbeispiel. Der Befehl im folgenden Beispiel führt jedoch mit einem Aufruf von <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>, und das Ergebnis wird zurückgegeben, als eine **System.Xml.XmlReader**. Klicken Sie dann das Beispiel füllt die <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> Objekt mit diesem **System.Xml.XmlReader** mit der <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A> Methode. Obwohl dieses Beispiel lädt der **System.Xml.XmlReader** sofort, konnte Sie zwischenspeichern, das XML, das der Reader auf einer Festplatte enthalten ist oder diese Daten in eine andere Anwendung durch Mittel vor dem Laden der Daten in einem Cellset dar.  
  
 [!code-cs[Adomd.NetClient#DemonstrateDisconnectedCellset](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_2.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 [Abrufen von Daten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [Abrufen von Daten mittels AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)   
 [Abrufen von Daten mittels XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)  
  
  
