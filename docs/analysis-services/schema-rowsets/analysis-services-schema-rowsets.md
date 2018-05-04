---
title: Analysis Services-Schemarowsets | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SSAS, data access interfaces
- Analysis Services data access interfaces, schema rowsets
- data access interfaces [Analysis Services]
- XML for Analysis, schema rowsets
- rowsets [Analysis Services], retrieving schema rowsets
- retrieving schema rowsets
- XMLA, schema rowsets
- rowsets [Analysis Services]
- schema rowsets [Analysis Services], retrieving
ms.assetid: 820d4b59-d428-4616-b792-c848e5da407e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6be6dd4c95d2c44400a202e12179cd1eb5757b2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services-Schemarowsets
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Schemarowsets sind vordefinierte Tabellen, die Informationen zu Analysis Services-Objekten und zum Serverstatus enthalten, einschließlich Datenbankschema, aktive Sitzungen, Verbindungen, Befehle und Aufträge, die auf dem Server ausgeführt werden. Sie können Schemarowsettabellen in einem XML/A-Skriptfenster in SQL Server Management Studio abfragen, eine DMV-Abfrage für ein Schemarowset ausführen oder eine benutzerdefinierte Anwendung erstellen, die Schemarowsetinformationen enthält (z. B. eine Berichterstellungsanwendung, durch die die Liste der verfügbaren Dimensionen abgerufen wird, die zum Erstellen eines Berichts verwendet werden können).  
  
> [!NOTE]  
>  Bei Verwendung von Schemarowsets im XML/A-Skripts, die Informationen, die in zurückgegeben wird die *Ergebnis* Parameter von der [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) Methode ist gemäß den in diesem Abschnitt beschriebenen rowsetspaltenlayouts strukturiert. Vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis-Anbieter (XMLA) werden die Rowsets unterstützt, die von der XML for Analysis-Spezifikation benötigt werden. Einige der standardmäßigen Schemarowsets für OLE DB, OLE DB für OLAP und OLE DB für Data Mining-Datenquellenanbieter werden vom XMLA-Anbieter ebenfalls unterstützt. Die unterstützten Rowsets werden in den folgenden Themen beschrieben.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[XML for Analysis-Schemarowsets](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)|Beschreibt die vom XMLA-Anbieter unterstützten XMLA-Rowsets.|  
|[OLE DB-Schemarowsets](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)|Beschreibt die vom XMLA-Anbieter unterstützten OLE DB-Schemarowsets.|  
|[OLE DB für OLAP-Schemarowsets](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)|Beschreibt die vom XMLA-Anbieter unterstützten OLE DB für OLAP-Schemarowsets.|  
|[Datamining-Schemarowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)|Beschreibt die vom XMLA-Anbieter unterstützten Data Mining-Schemarowsets.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenzugriff auf mehrdimensionale Modelle & #40; Analysis Services – mehrdimensionale Daten & #41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [Verwenden Sie dynamische Verwaltungssichten & #40; DMVs & #41; zum Überwachen von Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
