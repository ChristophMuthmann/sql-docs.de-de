---
title: "Unterstützte Datenquellen (SSAS – mehrdimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
caps.latest.revision: "69"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 69f1519d6b3c03294469707a7e1485955f864a2e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="supported-data-sources-ssas---multidimensional"></a>Unterstützte Datenquellen (SSAS – Mehrdimensional)
  In diesem Thema werden die Datenquellentypen beschrieben, die Sie in einem tabellarischen Modell verwenden können.  
  
##  <a name="bkmk_supported_ds"></a> Unterstützte Datenquellen  
 Sie können Daten aus den Datenquellen in der folgenden Tabelle abrufen. Bei der Installation von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]werden die für die einzelnen Datenquellen aufgelisteten Anbieter nicht von Setup installiert. Einige Anbieter wurden möglicherweise bereits mit anderen Anwendungen auf dem Computer installiert. In anderen Fällen müssen Sie den Anbieter herunterladen und installieren.  
  
> [!NOTE]  
>  Drittanbieterprodukte, wie z.&#160;B. der Oracle OLE DB-Anbieter, können ebenfalls verwendet werden, um eine Verbindung mit Drittanbieterdatenbanken herzustellen, wobei der Support vom entsprechenden Drittanbieter bereitgestellt wird.  
  
|||||  
|-|-|-|-|  
|Quelle|Versionen|Dateityp|Anbieter*|  
|Access-Datenbanken|Microsoft Access 2010, 2013, 2016|.accdb oder .mdb|Microsoft Jet 4.0 OLE DB-Anbieter|  
|Relationale SQL Server-Datenbanken*|Microsoft SQL Server 2008, 2008 R2, 2012, 2014, 2016, [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] , Microsoft Analytics Platform System (APS)<br /><br /> <br /><br /> Hinweis: Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Azure.com [finden Sie weitere Details zu](http://go.microsoft.com/fwlink/?LinkID=157856).<br /><br /> Hinweis: Das Analytics Platform System (APS) wurde früher als SQL Server Parallel Data Warehouse (PDW) bezeichnet. Ursprünglich war für das Herstellen einer Verbindung mit PDW von Analysis Services ein spezieller Datenanbieter erforderlich. Dieser Anbieter wurde in SQL Server 2012 ersetzt. Ab SQL Server 2012 wird der SQL Server Native Client für Verbindungen mit PDW/APS verwendet. Weitere Informationen zu APS finden Sie auf der Website [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx).|(–)|OLE DB-Anbieter für SQL Server<br /><br /> SQL Server Native Client OLE DB-Anbieter<br /><br /> OLE DB-Anbieter für SQL Server Native 11.0 Client<br /><br /> .NET Framework-Datenanbieter für SQL Client|  
|Relationale Oracle-Datenbanken|Oracle 9i, 10g, 11g, 12g|(–)|OLE DB-Anbieter für Oracle<br /><br /> .NET Framework-Datenanbieter für Oracle Client<br /><br /> .NET Framework-Datenanbieter für SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Relationale Teradata-Datenbanken|Teradata V2R6, V12|(–)|OLE DB-Anbieter für TDOLEDB<br /><br /> .NET-Datenanbieter für Teradata|  
|Relationale Informix-Datenbanken|V11.10|(–)|OLE DB-Anbieter für Informix|  
|Relationale IBM DB2-Datenbanken|8.1|(–)|DB2OLEDB|  
|Relationale Datenbanken von Sybase Adaptive Server Enterprise (ASE)|15.0.2|(–)|OLE DB-Anbieter für Sybase|  
|Andere relationale Datenbanken|(–)|(–)|Einen OLE DB-Anbieter.|  
  
 \* ODBC-Datenquellen werden für mehrdimensionale Lösungen nicht unterstützt. Zwar wird die Verbindung von Analysis Services selbst behandelt, doch können die in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] zum Erstellen von Lösungen verwendeten Designer keine Verbindung mit einer ODBC-Datenquelle auch dann nicht herstellen, wenn der MSDASQL-Treiber verwendet wird. Wenn die Geschäftsanforderungen eine ODBC-Datenquelle umfassen, erwägen Sie, stattdessen eine tabellarische Lösung zu erstellen.  
  
 **Für einige Funktionen ist eine lokal ausgeführte relationale SQL Server-Datenbank erforderlich. Insbesondere für Rückschreibevorgänge und ROLAP-Speicher muss die zugrunde liegende Datenquelle eine relationale SQL Server-Datenbank sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Datenquellen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
