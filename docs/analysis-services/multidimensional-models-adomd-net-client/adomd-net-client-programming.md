---
title: ADOMD.NET-Clientprogrammierung | Microsoft Docs
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
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [ADOMD.NET]
- ADOMD.NET, programming
ms.assetid: 55156115-ecd1-4ed9-876e-23406af9bbf9
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f6ed705a9cd5f4084dcf6e09b619431479a23826
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="adomdnet-client-programming"></a>ADOMD.NET-Clientprogrammierung
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die ADOMD.NET-Clientkomponenten befinden sich innerhalb der **Microsoft.AnalysisServices.AdomdClient** -Namespace (in microsoft.analysisservices.adomdclient.dll). Diese Clientkomponenten bieten Funktionen für Clientanwendungen und Anwendungen der mittleren Ebene auf einfachen Abfrage von Daten und Metadaten aus einer analytischen Datenspeichers, z. B. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="using-the-adomdnet-client-objects"></a>Verwenden der ADOMD.NET-Clientobjekte  
 Beim Abfragen der analytischen Datenquelle müssen mehrere gängige Tasks ausgeführt werden. Die folgende Tabelle stellt die gängigen Tasks dar, in denen Sie die ADOMD.NET-Clientobjekte zum Ausführen einer solchen Abfrage verwenden.  
  
|Task|Description|  
|----------|-----------------|  
|[Aufbauen von Verbindungen in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)|In ADOMD.NET wird das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt verwendet, um Verbindungen mit analytischen Datenquellen wie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbanken herzustellen. Sie können das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt verwenden, um Befehle auszuführen sowie Daten und Metadaten von der analytischen Datenquelle abzurufen.|  
|[Abrufen von Metadaten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)|Wenn eine Verbindung hergestellt wurde, stehen Ihnen zahlreiche verschiedene Objekte für die Abfrage von Informationen zu den zugrunde liegenden Datenquellen zur Verfügung. Diese Funktionalität ermöglicht es Anwendungen, sich an die Datenquelle anzupassen, mit der sie eine Verbindung hergestellt haben.|  
|[Ausführen von Befehlen für eine analytische Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)|Das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekt stellt die Schnittstellen bereit, die erforderlich sind, um Befehle für die zugrunde liegende analytische Datenquelle auszuführen.|  
|[Abrufen von Daten von einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)|Nach Ausführung ein Befehls abgerufen werden konnte und entweder analysierten Daten der <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, oder **System.XmlReader** Objekte.|  
|[Ausführen von Transaktionen in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-performing-transactions.md)|Alle in den vorherigen Zeilen dieser Tabelle aufgelisteten Aktionen können innerhalb einer Transaktion ausgeführt werden, bei der ein Commit vor dem Lesevorgang ausgeführt werden muss und in der freigegebene Sperren während des Lesens der Daten aufrechterhalten werden. Dadurch werden Dirty Reads verhindert. Die Daten können auch vor dem Ende der Transaktion noch geändert werden, was zu nicht wiederholbaren Lesevorgängen oder Phantomdaten führt. Das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>-Objekt stellt die Transaktionsfunktionalität in ADOMD.NET bereit.|  
  
 Die Interaktion mit der ADOMD.NET-Objekthierarchie beginnt normalerweise mit einem oder mehreren der Objekte auf der obersten Ebene, wie in der folgenden Tabelle erläutert.  
  
|Aktion|Verwenden Sie dieses Objekt|  
|--------|---------------------|  
|Herstellen einer Verbindung mit einer analytischen Datenquelle|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> Das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt stellt eine Verbindung zu einer Datenquelle und den Datenquellenmetadaten dar. Angenommen, Sie können eine Verbindung herstellen ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lokale Cubedatei (CUB) Datei, und überprüfen Sie die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> Eigenschaft zum Abrufen von Metadaten zu den Cubes, die für die analytische Datenquelle vorhanden. Dieses Objekt stellt auch die Implementierung der **IDbConnection** -Schnittstelle, eine Schnittstelle, die von allen .NET Framework-Datenanbietern benötigt wird.|  
|Ermitteln der Data Mining-Fähigkeiten der Datenquelle|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection><br /> Das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt macht mehrere Miningauflistungen verfügbar:<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> enthält eine Liste aller Miningmodelle in der Datenquelle.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> stellt Informationen über die verfügbaren Mining-Algorithmen bereit.<br /><br /><br /><br /> <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> macht Informationen über die Mining-Strukturen auf dem Server verfügbar.|  
|Abfragen der Datenquelle|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand><br /> Das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekt stellt die Anweisung oder die Abfrage dar, die an den Server gesendet wird. Wenn eine Verbindung mit einer Datenquelle hergestellt ist, wird ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekt verwendet, um Anweisungen in der unterstützten Sprache, wie Multidimensional Expressions (MDX) oder Data Mining Data Mining Extensions (DMX), auszuführen. Sie können auch ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekt verwenden, um Ergebnisse als <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>- oder <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>-Objekte zurückzugeben.|  
|Abrufen von Daten auf schnelle und effiziente Weise|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader><br /> Der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> kann durch Aufrufen der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A>- oder der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A>-Methode eines <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>-Objekts erstellt werden. Dieses Objekt implementiert die **IDbDataReader** -Schnittstelle aus dem **"System.Data"** Namespace der .NET Framework-Klassenbibliothek.|  
|Abrufen von analytischen Daten mit der größten Menge an Metadaten|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet><br /> Das <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> kann durch Aufrufen der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A>- oder der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>-Methode eines <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> erstellt werden. Sobald ein <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> ein <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> zurückgegeben hat, können Sie die im <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> enthaltenen analytischen Daten überprüfen.|  
|Abrufen von Metadaten über Cubes, z. B. verfügbare Dimensionen, Measures, benannte Mengen usw.|<xref:Microsoft.AnalysisServices.AdomdClient.CubeDef><br /> Die <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> stellt Metadaten eines Cubes dar. Auf die <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> können Sie über die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> verweisen.|  
|Abrufen von Daten mithilfe der **System.Data.IDbDataAdapter** Schnittstelle|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter><br /> Der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter> bietet schreibgeschützte Unterstützung für vorhandene .NET Framework-Clientanwendungen.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-serverprogrammierung](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)   
 [Entwickeln mit ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
  
