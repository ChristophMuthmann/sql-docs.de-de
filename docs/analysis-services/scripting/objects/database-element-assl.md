---
title: Database-Element (ASSL) | Microsoft Docs
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
apiname:
- Database Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DATABASE
helpviewer_keywords:
- Database element
ms.assetid: c3bc7eaf-ed0d-4395-a3b7-8d9cfacfe911
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8adf82361d2644531eafb3f7b611fb9614a67731
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="database-element-assl"></a>Database-Element (ASSL)
  Definiert eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Databases>  
   <Database>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastUpdate>...</LastUpdate>  
      <Description>...</Description>  
      <State>   </State>  
      <AggregationPrefix>...</AggregationPrefix>  
      <EstimatedSize>...</EstimatedSize>  
      <LastProcessed>...</LastProcessed>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <Visible>...</Visible>  
      <MasterDatasourceID>...</MasterDataSourceID>  
      <Accounts>...</Accounts>  
      <DataSources>...</DataSources>  
      <DataSourceViews>...</DataSourceViews>  
      <Dimensions>...</Dimensions>  
      <Cubes>...</Cubes>  
      <MiningStructures>...</MiningStructures>  
            <Roles>...</Roles>  
      <Assemblies>...</Assemblies>  
      <DatabasePermissions>...</DatabasePermissions>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Datenbanken](../../../analysis-services/scripting/collections/databases-element-assl.md)|  
|Untergeordnete Elemente|[Konten](../../../analysis-services/scripting/collections/accounts-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Assemblys](../../../analysis-services/scripting/collections/assemblies-element-assl.md), [Sortierung](../../../analysis-services/scripting/properties/collation-element-assl.md), [ CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [Cubes](../../../analysis-services/scripting/collections/cubes-element-assl.md), [DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md), [DataSources](../../../analysis-services/scripting/collections/datasources-element-assl.md), [DataSourceViews](../../../analysis-services/scripting/collections/datasourceviews-element-assl.md), [Beschreibung](../../../analysis-services/scripting/properties/description-element-assl.md), [Dimensionen](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Sprache](../../../analysis-services/scripting/properties/language-element-assl.md), [ LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [LastUpdate](../../../analysis-services/scripting/properties/lastupdate-element-assl.md), [MasterDatasourceID](../../../analysis-services/scripting/properties/masterdatasourceid-element-assl.md), [MiningStructures](../../../analysis-services/scripting/collections/miningstructures-element-assl.md), [Namen](../../../analysis-services/scripting/properties/name-element-assl.md), [Rollen](../../../analysis-services/scripting/collections/roles-element-assl.md), [Status](../../../analysis-services/scripting/properties/state-element-assl.md), [Übersetzungen](../../../analysis-services/scripting/collections/translations-element-assl.md), [sichtbar](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Database>.  
  
## <a name="see-also"></a>Siehe auch  
 [Server-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

