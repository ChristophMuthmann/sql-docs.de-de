---
title: Data Mining-Schemarowsets (SSAs) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
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
ms.topic: article
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 23f8b63c593e1269624905caf8809ac5afefd1d5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-schema-rowsets-ssas"></a>Data Mining-Schemarowsets (SSAs)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], viele der vorhandenen OLE DB-Datamining Schema Rowsets microservices wird als eine Reihe von Systemtabellen, die Sie mithilfe von Data Mining Extensions (DMX)-Anweisungen Abfragen können. Durch das Erstellen von Queries für das Data Mining-Schemarowset können Sie die zur Verfügung stehenden Services identifizieren, Statusupdates für Ihre Modelle und Strukturen erhalten und Details über den Inhalt des Modells oder Parameter erfahren. Eine Beschreibung des Data Mining-Schemarowsets finden Sie unter [Data Mining Schema Rowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md).  
  
> [!NOTE]  
>  Sie können auch das Data Mining-Schemarowset mithilfe von XMLA abfragen. Weitere Informationen dazu, wie Sie dies in SQL Server Management Studio tun, finden Sie unter [Erstellen einer Data Mining-Abfrage mit XMLA](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="list-of-data-mining-schema-rowsets"></a>Liste der Data Mining-Schemarowsets  
 In der folgenden Tabelle werden die Data Mining-Schemarowsets, die möglicherweise zum Abfragen und Überwachen nützlich sind, aufgelistet.  
  
|Rowsetname|Description|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS-Rowset|Listet alle Miningmodelle im aktuellen Kontext auf.<br /><br /> Beinhaltet Informationen wie das Erstellungsdatum, Parameter, die zur Erstellung des Modells verwendet wurden, und die Größe des Trainingsatzes.|  
|DMSCHEMA_MINING_COLUMNS|Listet alle in Miningmodellen verwendeten Spalten im aktuellen Kontext auf.<br /><br /> Zu den Informationen gehören das Zuordnen der Quellspalte der Miningstruktur, der Datentyp, die Genauigkeit und Vorhersagefunktionen, die mit der Spalte verwendet werden können.|  
|DMSCHEMA_MINING_STRUCTURES|Listet alle Miningstrukturen im aktuellen Kontext auf.<br /><br /> Hierzu gehören Informationen darüber, ob die Struktur Daten enthält, das Datum der letzten Verarbeitung der Struktur und gegebenenfalls die Definition des zurückgehaltenen Datasets.|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|Listet alle in Miningstrukturen verwendeten Spalten im aktuellen Kontext auf.<br /><br /> Zu den Informationen gehören Inhaltstyp und Datentyp, NULL-Zulässigkeit und ob die Spalte geschachtelte Tabellendaten enthält.|  
|DMSCHEMA_MINING_SERVICES|Listet alle Miningdienste oder Algorithmen, die auf dem angegebenen Server verfügbar sind, auf.<br /><br /> Informationen enthalten unterstützte Modellierungsflags, Eingabetypen und unterstützte Datenquellentypen.|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|Listet alle Parameter für die Miningdienste, die auf der angegebenen Instanz verfügbar sind, auf.<br /><br /> Die Informationen enthalten den Datentyp für jeden Parameter, die Standardwerte und die oberen und unteren Grenzen.|  
|DMSCHEMA_MODEL_CONTENT|Gibt den Inhalt des Modells zurück, wenn das Modell verarbeitet wurde.<br /><br /> Weitere Informationen finden Sie unter [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).|  
|DBSCHEMA_CATALOGS|Listet alle Datenbanken (Kataloge) in der aktuellen Instanz von Analysis Services auf.|  
|MDSCHEMA_INPUT_DATASOURCES|Listet alle Datenquellen in der aktuellen Instanz von Analysis Services auf.|  
  
> [!NOTE]  
>  Die Liste in der Tabelle ist nicht vollständig; es werden nur die Rowsets angezeigt, die für die Problembehandlung am wichtigsten sein könnten.  
  
## <a name="examples"></a>Beispiele  
 Der folgende Abschnitt enthält einige Beispiele für Abfragen gegen die Data Mining-Schemarowsets.  
  
### <a name="example-1-list-data-mining-services"></a>Beispiel 1: Auflisten von Data Mining-Diensten  
 Die folgende Abfrage gibt eine Liste der Miningdienste zurück, die auf dem aktuellen Server zur Verfügung stehen, d. h. die aktivierten Algorithmen. Die für jeden Miningdienst bereitgestellten Spalten beinhalten die Modellierungsflags und Inhaltstypen, die von jedem Algorithmus verwendet werden können, die GUID für jeden Dienst und jegliche Vorhersagenbeschränkungen, die für jeden Dienst hinzugefügt worden sein könnten.  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>Beispiel 2: Auflisten von Miningmodellparametern  
 Das folgende Beispiel gibt die Parameter zurück, die verwendet wurden, um ein bestimmtes Miningmodell zu erstellen.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>Beispiel 3: Auflisten aller Rowsets  
 Im folgenden Beispiel wird eine umfassende Liste der Rowsets, die auf dem aktuellen Server verfügbar sind, zurückgegeben:  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
  
