---
title: Abrufen von Daten aus einer analytischen Datenquelle | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f8d2c400fc82852333b64d9bd89b2e7c74190061
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>Abrufen von Daten von einer analytischen Datenquelle
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Nachdem Sie eine Verbindung herstellen und die Abfrage erstellen, können keine Daten abgerufen werden. In ADOMD.NET können Sie Daten über drei Objekte abrufen (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, und <xref:System.Xml.XmlReader>) durch einen Aufruf der der **Execute** Methoden die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> Objekt.  
  
 Jedes dieser drei Objekte stellt ein Gleichgewicht zwischen Interaktivität und Aufwand her:  
  
-   *Interaktivität* bezieht sich auf die einfach zu verwendende und die Menge an Informationen über das Objektmodell zur Verfügung.  
  
-   *Aufwand* bezieht sich auf die Menge des Datenverkehrs, der ein Objektmodell generiert wird, über die Netzwerkverbindung mit dem Server, der benötigte Speicherplatz für das Objektmodell und die Geschwindigkeit, mit denen das Objektmodell Daten abruft.  
  
 Um Sie bei der Auswahl des Datenabrufobjekts, das am geeignetsten für die Anforderungen Ihrer Anwendung ist, zu unterstützen, stellt die folgende Tabelle die Unterschiede zwischen Interaktivität und Aufwand für jedes Objekt heraus.  
  
|Objekt|Interaktivität|Verwaltungsaufwand|Behält Dimensionalität bei|Informationen zur Verwendung|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|Am höchsten|Mittelhoch, führt zum langsamsten Datenabruf|ja|[Abrufen von Daten mit dem Cellset](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|"Mittel"|"Mittel"|Nein|[Auffüllen eines Datasets mit "DataAdapter"](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|"Mittel"|"Mittel"|Nein|[Abrufen von Daten mittels AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|Am niedrigsten|Am niedrigsten, was zum schnellsten Datenabruf führt|ja|[Abrufen von Daten mittels XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Clientprogrammierung](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
