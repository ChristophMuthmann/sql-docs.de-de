---
title: Partitions-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Partition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90c86a43bbd290ae3ffd04408ab61a68a307fc83
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="partition-element-assl"></a>Partition-Element (ASSL)
  Definiert eine Partition eine [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) Element oder eine partitionsbindung in einem Out-of-Line [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Partitions>  
      <Partition> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Source>...</Source>  
      <ProcessingPriority>...</ProcessingPriority>  
      <AggregationPrefix>...</AggregationPrefix>  
      <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <StorageLocation>...</StorageLocation>  
      <RemoteDatasourceID>...</RemoteDatasourceID>  
      <Slice>...</Slice>  
      <ProactiveCaching>...</ProactiveCaching>  
      <Type>...</Type>  
      <EstimatedSize>...</EstimatedSize>  
      <EstimatedRows>...</EstimatedRows>  
      <CurrentStorageMode>...</CurrentStorageMode>  
      <AggregationDesignID>...</AggregationDesignID>  
      <AggregationInstances>...</AggregationInstances>  
      <AggregationInstanceSource>...</AggregationInstanceSource>  
      <LastProcessed>...</LastProcessed>  
      <State>...</State>  
      <Annotations>.../Annotations>  
   </Partition>  
   <!-- or -->  
   <Partition xsi:type="PartitionBinding"> <!-- ancestor: MeasureGroupBinding -->  
   </Partition>  
</Partitions>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Finden Sie in der folgenden Tabelle aus.|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
|Vorgänger oder übergeordnetes Element|Datentyp|  
|------------------------|---------------|  
|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Keine|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Partitionen](../../../analysis-services/scripting/collections/partitions-element-assl.md)|  
|Untergeordnete Elemente|Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgänger oder übergeordnetes Element|Untergeordnete Elemente|  
|------------------------|--------------------|  
|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md), [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md), [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md), [Beschreibung](../../../analysis-services/scripting/properties/description-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [ EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ Namen](../../../analysis-services/scripting/properties/name-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md), [Slice](../../../analysis-services/scripting/properties/slice-element-assl.md), [Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Status](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [Typ](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Diesem Element sind unter dem DeploymentMode-Wert 2 (tabellarischer Servermodus) die folgenden Überprüfungen zugeordnet:  
  
-   Die folgenden untergeordneten Elemente werden nicht unterstützt und sollten nicht verwendet werden:  
  
    -   [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)  
  
    -   [Slice](../../../analysis-services/scripting/properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
    -   [Typ](../../../analysis-services/scripting/properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)  
  
    -   [AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)  
  
     Ein Fehler könnte ausgelöst werden, wenn eines der oben genannten Elemente verwendet wird.  
  
-   Die [Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md) -Element akzeptiert nur **Abfrage** Bindung.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

