---
title: StorageEngineUsed-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- StorageEngineUsed Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
ms.assetid: 98895c10-f3c2-4d8a-be94-6128c828561d
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 188c9261964839c055b75e2abb4c1e8fc4ec3633
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="storageengineused-element-xmla"></a>StorageEngineUsed-Element (XMLA)
  Enthält einen schreibgeschützten Wert, der den aktuellen Datenbanktyp angibt.  
  
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
            <StorageEngineUsed >...</StorageEngineUsed>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[database](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Herkömmliche*|Das Datenbankmodell entspricht dem MOLAP-, ROLAP- oder HOLAP-Speichermodus.|  
|*InMemory*|Das Datenbankmodell entspricht dem IMBI-Speichermodus.|  
|*Gemischt*|Das Datenbankmodell kombiniert IMBI- und MOLAP-, ROLAP- oder HOLAP-Speichermodi.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **"storageengineused"** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.StorageEngineUsed>.  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **"storageengineused"** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.Database>.  
  
  

