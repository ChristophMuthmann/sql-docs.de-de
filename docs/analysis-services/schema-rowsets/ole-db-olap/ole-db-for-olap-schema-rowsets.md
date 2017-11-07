---
title: "OLE DB für OLAP-Schemarowsets | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 655e40afe2808b5f26216923d54e474054170a54
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLE DB für OLAP-Schemarowsets
  Die folgenden OLE DB für OLAP-Schemarowsets werden vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis-Anbieter (XMLA) unterstützt.  
  
> [!NOTE]  
>  Verwenden Sie zum Überprüfen, ob ein bestimmter Datenquellenanbieter ein Rowset unterstützt die **DISCOVER_ENUMERATIONS** Rowset mit der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode.  
  
 Sie erhalten auch ausführliche Informationen über diese Rowsets finden Sie im Thema "OLAP-Schemarowsets" Suchen in der MSDN Library auf dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkId=15426).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Schemarowset<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[DISCOVER_INSTANCES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|Beschreibt die Instanzen auf dem Server.|  
|[DISCOVER_KEYWORDS-Rowset &#40; OLE DB für OLAP- &#41;](../../../analysis-services/schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)|Listet eine Liste von vom Anbieter reservierten Wörtern auf.|  
|[MDSCHEMA_ACTIONS-Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)|Beschreibt die Aktionen, die der Clientanwendung möglicherweise zur Verfügung stehen.|  
|[MDSCHEMA_CUBES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|Beschreibt die Struktur der Cubes innerhalb einer Datenbank.|  
|[MDSCHEMA_DIMENSIONS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|Beschreibt die freigegebenen und privaten Dimensionen innerhalb einer Datenbank.|  
|[MDSCHEMA_FUNCTIONS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|Beschreibt die Funktionen, die mit der Datenbank verbundene Clientanwendungen zur Verfügung stehen.|  
|[MDSCHEMA_HIERARCHIES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|Beschreibt jede Hierarchie, die in einer bestimmten Dimension enthalten ist.|  
|[MDSCHEMA_INPUT_DATASOURCES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|Beschreibt die innerhalb der Datenbank definierten Datenquellen.|  
|[MDSCHEMA_KPIS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|Beschreibt die Key Performance Indicators (KPIs) innerhalb einer Datenbank.|  
|[MDSCHEMA_LEVELS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|Beschreibt jede Ebene innerhalb einer bestimmten Hierarchie.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|Listet die Dimensionen der Measuregruppe auf.|  
|[MDSCHEMA_MEASUREGROUPS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|Beschreibt die Measuregruppen innerhalb einer Datenbank.|  
|[MDSCHEMA_MEASURES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|Beschreibt jedes Measure in einem Cube.|  
|[MDSCHEMA_MEMBERS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|Beschreibt die Elemente innerhalb einer Datenbank.|  
|[MDSCHEMA_PROPERTIES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|Beschreibt die Eigenschaften von Elementen in einer Datenbank.|  
|[MDSCHEMA_SETS-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|Beschreibt alle Sätze, die zurzeit in einer Datenbank definiert werden, einschließlich Sätzen im Bereich einer Sitzung.|  
  
 <sup>1</sup> alle hier aufgeführten Rowsets werden von der MSOLAP-Datenquellenanbieter für unterstützt die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA-Anbieter.  
  
## <a name="see-also"></a>Siehe auch  
 [DISCOVER_ENUMERATORS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

