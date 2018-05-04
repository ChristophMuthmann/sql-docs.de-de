---
title: Abrufen von Daten aus einer analytischen Datenquelle | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 91976fcd4f3922041152fe41c0e03f89e05483b2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>Abrufen von Daten von einer analytischen Datenquelle
  Sobald Sie eine Verbindung herstellen und die Abfrage erstellen, können Sie alle Daten abrufen. In ADOMD.NET können Sie Daten über drei Objekte abrufen (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, und <xref:System.Xml.XmlReader>) durch einen Aufruf der der **Execute** Methoden die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> Objekt.  
  
 Jedes dieser drei Objekte stellt ein Gleichgewicht zwischen Interaktivität und Aufwand her:  
  
-   *Interaktivität* bezieht sich auf die einfach zu verwendende und die Menge an Informationen über das Objektmodell zur Verfügung.  
  
-   *Aufwand* bezieht sich auf die Menge des Datenverkehrs, der ein Objektmodell generiert wird, über die Netzwerkverbindung mit dem Server, der benötigte Speicherplatz für das Objektmodell und die Geschwindigkeit, mit denen das Objektmodell Daten abruft.  
  
 Um Sie bei der Auswahl des Datenabrufobjekts, das am geeignetsten für die Anforderungen Ihrer Anwendung ist, zu unterstützen, stellt die folgende Tabelle die Unterschiede zwischen Interaktivität und Aufwand für jedes Objekt heraus.  
  
|Objekt|Interaktivität|Verwaltungsaufwand|Behält Dimensionalität bei|Informationen zur Verwendung|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|Am höchsten|Mittelhoch, führt zum langsamsten Datenabruf|ja|[Abrufen von Daten mit dem Cellset](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|"Mittel"|"Mittel"|nein|[Auffüllen eines Datasets mit "DataAdapter"](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|"Mittel"|"Mittel"|nein|[Abrufen von Daten mittels AdomdDataReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|Am niedrigsten|Am niedrigsten, was zum schnellsten Datenabruf führt|ja|[Abrufen von Daten mittels XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Clientprogrammierung](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
