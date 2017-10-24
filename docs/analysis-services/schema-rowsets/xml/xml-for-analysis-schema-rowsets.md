---
title: XML for Analysis-Schemarowsets | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- rowsets [Analysis Services], XML for Analysis
- XML for Analysis, schema rowsets
- schema rowsets [Analysis Services], XML for Analysis
- schema rowsets [XML for Analysis]
ms.assetid: 36e3ecfd-fcc3-415a-9c43-f59921d2468a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0c44abd2ba4be59a86b46a9b0ff74196c570e5e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis Schema Rowsets
  Der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA-Anbieter (XML for Analysis) schließt Schemarowsets ein, die Metadaten zu Serverstatus, Aktivität und Objekten zurückgeben. Es ist nötig, Metadaten abzurufen, wenn Sie eine Clientanwendung entwickeln, die eine Verbindung mit einem Analysis Services-Modell herstellt, dessen Struktur und Eigenschaften variabel sind.  
  
 Schemarowsets gewähren auch Einblicke in interne Prozesse und Vorgänge, die Ihnen helfen können, den Server zu überwachen und Probleme zu beheben. Sie können für die meisten Schemarowsets eine DMV-Abfrage (Dynamic Management View, dynamische Verwaltungssicht) ausführen, um administrative Ad-hoc-Aufgaben besser zu unterstützen. DMV-Abfragen geben Ergebnisse in einem lesbaren, tabellarischen Format zurück, das Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] anzeigen können.  
  
 In der folgenden Tabelle sind sämtliche XMLA-Schemarowsets sowie deren Beschreibungen enthalten. Zudem wird darin angegeben, ob Informationen zu tabellarischen Datenmodellen zurückgegeben werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Rowset<sup>1</sup>|Description|  
|------------------------|-----------------|  
|[DISCOVER_CALC_DEPENDENCY-Rowset](../../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|Gibt Informationen zu Abhängigkeiten unter Tabellen, Spalten, Measures und berechneten Spaltenformeln zurück.<br /><br /> Gilt für tabellarische Modelle auf einer Analysis Services-Instanz bereitgestellt und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Modelle in Excel-Arbeitsmappen, die in einer SharePoint-Umgebung ausgeführt.|  
|[DISCOVER_CONNECTIONS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|Stellt Informationen zur Ressourcenverwendung und Aktivität der zurzeit geöffneten Verbindungen auf dem Server bereit.|  
|[DISCOVER_COMMAND_OBJECTS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|Stellt Ressourcenverwendungs- und Aktivitätsinformationen über die Objekte bereit, die durch den Befehl, auf den verwiesen wird, verwendet werden.|  
|[DISCOVER_COMMANDS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|Stellt Ressourcenverwendungs- und Aktivitätsinformationen über die zurzeit oder zuletzt ausgeführten Befehle im Rahmen der aktiven Verbindungen auf dem Server bereit.|  
|[DISCOVER_CSDL_METADATA-Rowset](../../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|Gibt eine XML-Definition einer Datenquelle an einen Client, die einer tabellarischen nutzen können oder [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modellieren und die Quelldaten als Teil eines Berichts präsentieren.<br /><br /> Gilt für tabellarische Modelle auf einer Analysis Services-Instanz bereitgestellt und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Modelle in Excel-Arbeitsmappen, die in einer SharePoint-Umgebung ausgeführt.|  
|[DISCOVER_DATASOURCES-Rowset](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)|Gibt eine Liste der XMLA-Anbieterdatenquellen zurück, die auf dem Server oder dem Webdienst verfügbar sind.|  
|[DISCOVER_DB_CONNECTIONS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|Stellt Informationen zur Ressourcenauslastung und Aktivität der zurzeit geöffneten Verbindungen vom Server in einer Datenbank bereit.|  
|[DISCOVER_DIMENSION_STAT-Rowset](../../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|Gibt Statistiken zur angegebenen Dimension zurück.|  
|[DISCOVER_ENUMERATORS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|Gibt eine Liste mit Namen, Datentypen und Enumerationswerten von Enumeratoren zurück, die vom XMLA-Anbieter für eine bestimmte Datenquelle unterstützt werden.|  
|[DISCOVER_JOBS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|Stellt Informationen über die aktiven Aufträge bereit, die auf dem Server ausgeführt werden.|  
|[DISCOVER_KEYWORDS-Rowset &#40; XMLA &#41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|Gibt Informationen über vom XMLA-Anbieter reservierte Schlüsselwörter zurück.|  
|[DISCOVER_LITERALS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|Gibt Informationen zu Literalen zurück, einschließlich Datentypen und Werten, die vom XMLA-Anbieter unterstützt werden.|  
|[DISCOVER_LOCATIONS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-locations-rowset.md)|Gibt Informationen zum Inhalt einer Sicherungsdatei zurück.|  
|[DISCOVER_LOCKS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|Stellt Informationen über die aktuellen Sperren auf dem Server bereit.|  
|[DISCOVER_MEMORYGRANT-Rowset](../../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|Gibt eine Liste interner Arbeitsspeicherkontingent-Erteilungen zurück, die von Aufträgen in Anspruch genommen werden, die derzeit auf dem Server ausgeführt werden.|  
|[DISCOVER_MEMORYUSAGE-Rowset](../../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|Gibt die Speicherauslastungsstatistiken für verschiedene vom Server zugeordnete Objekte zurück.|  
|[DISCOVER_OBJECT_ACTIVITY-Rowset](../../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|Stellt die Ressourcenverwendung pro Objekt seit dem Start des Diensts bereit.|  
|[DISCOVER_OBJECT_MEMORY_USAGE-Rowset](../../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|Stellt Informationen über von Objekten verwendete Speicherressourcen bereit.|  
|[DISCOVER_PARTITION_DIMENSION_STAT-Rowset](../../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|Gibt Statistiken für die Dimension, die einer Partition zugeordnet ist.|  
|[DISCOVER_PARTITION_STAT-Rowset](../../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|Gibt Statistiken zu Aggregationen in einer bestimmten Partition zurück.|  
|[DISCOVER_PERFORMANCE_COUNTERS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|Gibt den Wert von mindestens einem angegebenen Leistungsindikator zurück.|  
|[DISCOVER_PROPERTIES-Rowset](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|Gibt eine Liste mit Informationen und Werten zu den standardmäßigen und anwenderspezifischen Eigenschaften zurück, die vom XMLA-Anbieter für die angegebene Datenquelle unterstützt werden.|  
|[DISCOVER_SCHEMA_ROWSETS-Rowsets](../../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|Gibt die Namen, Einschränkungen, Beschreibungen und anderen Informationen für alle Enumerationswerte und zusätzliche anbieterspezifische Enumerationswerte zurück, die vom XMLA-Anbieter unterstützt werden.|  
|[DISCOVER_SESSIONS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|Stellt Informationen zur Ressourcenverwendung und Aktivität der zurzeit geöffneten Sitzungen auf dem Server bereit.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|Stellt Informationen zu den auf Spalten- und Segmentebene Speichertabellen, die von einer tabellarischen verwendeten bereit oder [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Datenbank.<br /><br /> Gilt für tabellarische Modelle auf einer Analysis Services-Instanz bereitgestellt und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Modelle in Excel-Arbeitsmappen, die in einer SharePoint-Umgebung ausgeführt.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|Ermöglicht dem Client die Zuweisung von Spalten zu Speichertabellen, die von einer tabellarischen verwendet oder [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Datenbank.<br /><br /> Gilt für tabellarische Modelle auf einer Analysis Services-Instanz bereitgestellt und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Modelle in Excel-Arbeitsmappen, die in einer SharePoint-Umgebung ausgeführt.|  
|[DISCOVER_STORAGE_TABLES-Rowset](../../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|Gibt Informationen zu den in einem Modell verwendeten Tabellen zurück.<br /><br /> Gilt für tabellarische Modelle auf einer Analysis Services-Instanz bereitgestellt und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Modelle in Excel-Arbeitsmappen, die in einer SharePoint-Umgebung ausgeführt.|  
|[DISCOVER_TRACE_COLUMNS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|Beschreibt die vom Ablaufverfolgungsanbieter bereitgestellten Ablaufverfolgungsspalten.|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO-Rowset](../../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|Gibt grundlegende Informationen zum Ablaufverfolgungsanbieter zurück, beispielsweise dessen Name und Beschreibung.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES-Rowset](../../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|Beschreibt die vom Ablaufverfolgungsanbieter bereitgestellten Ereigniskategorien.|  
|[DISCOVER_TRACES-Rowset](../../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|Gibt Informationen zu Ablaufverfolgungen zurück, die auf einem Server ausgeführt werden.|  
|[DISCOVER_TRANSACTIONS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|Gibt den aktuellen Satz von ausstehenden Transaktionen auf dem System zurück.|  
|[DISCOVER_XML_METADATA-Rowset](../../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)|Gibt ein XML-Dokument zurück, in dem ein angefordertes Objekt beschrieben wird.|  
  
 <sup>1</sup> alle hier aufgeführten Rowsets werden von der MSOLAP-Datenquellenanbieter für unterstützt die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA-Anbieter.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit XMLA in Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Verwenden Sie dynamische Verwaltungssichten &#40; DMVs &#41; zum Überwachen von Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [Abrufen von Metadaten aus einer analytischen Datenquelle](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  

