---
title: "Ausführen von Befehlen für eine analytische Datenquelle | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 810c6e8bd489bac42a3f4d90d4dbe9990f5ca038
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="executing-commands-against-an-analytical-data-source"></a>Ausführen von Befehlen für eine analytische Datenquelle
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Nachdem eine Verbindung mit einer analytischen Datenquelle hergestellt wurde, können Sie ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> Objekt, das Befehle gegen ausführen und Ergebnisse aus dieser Datenquelle zurück. Diese Befehle können mithilfe von multidimensionalen Ausdrücken (Multidimensional Expressions, MDX), Data Mining-Erweiterungen (DMX) oder einer begrenzten SQL-Syntax Daten abrufen. Darüber hinaus können Sie ASSL-Befehle (Analysis Services Scripting Language) verwenden, um die zugrunde liegende Datenbank zu bearbeiten.  
  
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
  
  
