---
title: Abrufen von Daten mittels XmlReader | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e94ac318753a8f0684d3ccb43e0e079521c8828b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="retrieving-data-using-the-xmlreader"></a>Abrufen von Daten mittels XmlReader
  Die **XmlReader** Klasse, die Bestandteil von der **"System.xml"** Namespace-URI für die Microsoft .NET Framework-Klassenbibliothek, ähnelt der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> -Klasse insofern, die **XmlReader**Klasse, bietet auch schnellen, nicht zwischengespeicherten, nur vorwärts Zugriff auf Daten. Wenn keine Notwendigkeit für eine in-Memory-analytische Ansicht der Daten unter Verwendung besteht der <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> -Objekt, das **XmlReader** Objekt ist ideal zum Abrufen von XML-Daten, insbesondere bei großer Mengen von Daten. Da **XmlReader** streamt Daten **XmlReader** keine abruft und alle Daten vor Offenlegung der Daten an den Aufrufer zwischenspeichert, als wäre der Fall, wenn ein <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> -Objekt wurden zum Konvertieren der XML for Analysis-Antwort in eine analytische objektmodelldarstellung.  
  
 Die **XmlReader** Klasse bietet direkten Zugriff auf die XML for Analysis-Antwort von ADOMD.NET empfangene bei der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> Methode der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> -Objekts aufgerufen wird. Da es sich bei den abgerufenen Daten um nicht formatierte XML-Rohdaten handelt, müssen Sie die Daten und Metadaten manuell analysieren. Sobald die Daten abgerufen wurden, die **XmlReader** Objekt geschlossen werden sollen.  
  
## <a name="retrieving-data-and-metadata"></a>Abrufen von Daten und Metadaten  
 Verwenden der **XmlReader** -Klasse zum Abrufen von Daten, Sie gehen Sie folgendermaßen vor:  
  
1.  **Erstellen Sie eine neue Instanz des Objekts.**  
  
     So erstellen eine neue Instanz der der **XmlReader** -Klasse, rufen Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> oder <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> Methode der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> Objekt.  
  
2.  **Abrufen von Daten.**  
  
     Nachdem der Befehl führt die Abfrage aus und gibt eine **XmlReader**, müssen Sie die Daten und Metadaten analysieren. Die XML-Daten und -Metadaten werden im systemeigenen Format angegeben, das vom XML for Analysis-Anbieter verwendet wird. Für die meisten XML for Analysis-Anbieter das systemeigene Format ist die **MDDataSet** Format. Die **MDDataSet** -Format bietet Daten und Metadaten für Cellsets in einem gut strukturierten Format. Weitere Informationen zu den **MDDataSet** formatieren, finden Sie in der XML for Analysis-Spezifikation.  
  
3.  **Schließen des Readers an.**  
  
     Sie sollten immer aufrufen, die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> Methode, wenn Sie aufgehört haben die **XmlReader** Objekt. Während einer **XmlReader** geöffnet, die **XmlReader** bietet die exklusive Verwendung des der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> -Objekt, das zum Ausführen des Befehls verwendet wurde. Sie werden nicht in der Lage sind, führen Sie Befehle mithilfe dieses <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, einschließlich der Erstellung eines weiteren **XmlReader** oder <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, bis Sie die ursprüngliche schließen **XmlReader**.  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>Beispiel für das Abrufen von Daten aus XmlReader  
 Im folgenden Beispiel wird ein Befehl ausgeführt, und ruft die Daten als ein **XmlReader**, den Inhalt der Datei an die Konsole ausgeben.  
  
 [!code-cs[Adomd.NetClient#OutputDataWithXML](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_1_1.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 [Abrufen von Daten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [Abrufen von Daten mittels CellSet](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [Abrufen von Daten mittels AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)  
  
  
