---
title: Data Mining-Schemarowsets | Microsoft Docs
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
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fcde375ccb8186f0ef5d38dca2c7f88aefaaf4b7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Ein Server mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt folgende Data mining-Schemarowsets. Verwenden Sie zum Überprüfen, ob ein bestimmter XML/A-Anbieter ein bestimmtes Rowset unterstützt die [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) Rowset mit der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode.  
  
 In [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]werden die Data mining Schema Rowsets als Tabellen in der Transact-SQL-Sprache im Schema $SYSTEM verfügbar gemacht werden. Die folgende Abfrage einer Analysis Services-Instanz gibt eine Liste der Schemas zurück, die auf der aktuellen Instanz verfügbar sind.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Schemarowset|Description|  
|-------------------|-----------------|  
|[DMSCHEMA_MINING_COLUMNS-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|Beschreibt die einzelnen Spalten aller definierten Data Mining-Modelle, die auf dem Server verteilt werden.|  
|[DMSCHEMA_MINING_FUNCTIONS-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|Beschreibt die Vorhersagefunktionen und Miningfunktionen, die mit jedem Data Mining-Algorithmus verwendet werden können, der auf dem Server installiert ist.|  
|[DMSCHEMA_MINING_MODEL_CONTENT-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|Ermöglicht es der Clientanwendung, den Inhalt eines trainierten Data Mining-Modells zu durchsuchen.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|Gibt die XML-Darstellung (PMML 2.1) des Miningmodellinhalts wieder.|  
|[DMSCHEMA_MINING_MODEL_XML-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|Gibt die XML-Struktur (PMML 2.1) des Miningmodells wieder. Dies ist das gleiche Schema wie DMSCHEMA_MINING_MODEL_PMML, das aus Gründen der Abwärtskompatibilität beibehalten wurde.|  
|[DMSCHEMA_MINING_MODELS-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|Listet die Data Mining-Modelle auf, die auf dem Server verteilt werden.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|Stellt eine Liste von Parametern bereit, die zur Konfiguration des Verhaltens eines jeden auf dem Server installierten Data Mining-Algorithmus verwendet werden kann.|  
|[DMSCHEMA_MINING_SERVICES-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|Stellt eine Beschreibung aller Data Mining-Algorithmen bereit, die auf dem Server verfügbar sind.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|Beschreibt die einzelnen Spalten aller Data Mining-Strukturen, die auf dem Server verteilt werden.|  
|[DMSCHEMA_MINING_STRUCTURES-Rowset](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|Listet Informationen zu Miningstrukturen auf.|  
  
 Alle hier aufgeführten Rowsets werden unterstützt, durch den Server mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Datamining-Schemarowsets &#40; SSAs &#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
