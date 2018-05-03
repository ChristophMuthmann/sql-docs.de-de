---
title: Ausführen von Befehlen für eine analytische Datenquelle | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2255f699edf57b1416191383b216875a7f13bb5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="executing-commands-against-an-analytical-data-source"></a>Ausführen von Befehlen für eine analytische Datenquelle
  Wenn eine Verbindung zu einer analytischen Datenquelle hergestellt wurde, können Sie ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekt verwenden, um Befehle für diese Datenquelle auszuführen und Ergebnisse von der Datenquelle zurückzugeben. Diese Befehle können mithilfe von multidimensionalen Ausdrücken (Multidimensional Expressions, MDX), Data Mining-Erweiterungen (DMX) oder einer begrenzten SQL-Syntax Daten abrufen. Darüber hinaus können Sie ASSL-Befehle (Analysis Services Scripting Language) verwenden, um die zugrunde liegende Datenbank zu bearbeiten.  
  
## <a name="creating-a-command"></a>Erstellen eines Befehls  
 Vor dem Ausführen eines Befehls müssen Sie diesen erstellen. Sie können einen Befehl auf zwei verschiedene Arten erstellen:  
  
-   Die erste Methode verwendet den <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Konstruktor, der das Ausführen eines Befehls für die Datenquelle ermöglicht sowie ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt angibt, auf dem der Befehl ausgeführt wird.  
  
-   Die zweite Methode verwendet die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.CreateCommand%2A>-Methode des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekts.  
  
 Der Text des auszuführenden Befehls kann abgefragt und mit der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.CommandText%2A>-Eigenschaft bearbeitet werden. Die Befehle, die Sie erstellen, müssen keine Daten zurückgeben, nachdem sie ausgeführt wurden.  
  
## <a name="running-a-command"></a>Ausführen eines Befehls  
 Wenn Sie ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekt erstellt haben, stehen mehrere <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A>-Methoden zur Verfügung, die Ihr Befehl zum Ausführen verschiedener Aktionen verwenden kann. In der folgenden Tabelle werden einige dieser Aktionen aufgeführt.  
  
|Aktion|Verwenden Sie diese Methode|  
|--------|---------------------|  
|Zurückgeben von Ergebnissen als Datenstrom|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A>, um ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>-Objekt zurückzugeben|  
|Zurückgeben eines <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>-Objekts|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>|  
|Ausführen von Befehlen, die keine Zeilen zurückgeben|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery%2A>|  
|Zurückgeben einer **XMLReader** Objekt, das die Daten in XML for Analysis (XMLA) kompatiblen Format enthält.|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>Beispiel für das Ausführen eines Befehls  
 Dieses Beispiel verwendet die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> XMLA-Befehl ausführen, die verarbeitet die **Adventure Works DW** Cube auf dem lokalen Server, ohne Daten zurückzugeben.  
  
 [!code-cs[Adomd.NetClient#ExecuteXMLAProcessCommand](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/executing-commands-again_1.cs)]  
  
  
