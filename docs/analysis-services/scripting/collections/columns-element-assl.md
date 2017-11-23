---
title: Columns-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Columns Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: COLUMNS
helpviewer_keywords: Columns element
ms.assetid: 14011eed-6f10-4120-b256-d599d59bde80
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 55467e21f97a6bb3bbef079ce19b2fa8dc345ca8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="columns-element-assl"></a>Columns-Element (ASSL)
  Enthält die Auflistung der Spalten, die mit dem übergeordneten Element verknüpft sind.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action xsi:type="DrillThroughAction"> <!-- or one of the elements listed below in the Element Relationships table -->  
   <Columns>  
      <Column xsi:type="MeasureBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="EventColumn">...</Column> <!-- parent: Event -->  
      <!-- or -->  
      <Column xsi:type="MiningModelColumn">...</Column> <!-- parent: MiningModel or MiningModelColumn -->  
      <!-- or -->  
      <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent: MiningStructure or TableMiningStructureColumn -->  
   </Columns>  
</DrillThroughAction>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Cardinality|Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgänger oder übergeordnetes Element|Cardinality|  
|------------------------|-----------------|  
|[Ereignis](../../../analysis-services/scripting/objects/event-element-assl.md)|1-1: Erforderliches Element, das nur einmal auftritt.|  
|Alle sonstigen|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) des Typs [DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [Ereignis](../../../analysis-services/scripting/objects/event-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|  
|Untergeordnete Elemente|Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgänger oder übergeordnetes Element|Untergeordnete Elemente|  
|------------------------|--------------------|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md) oder [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[Ereignis](../../../analysis-services/scripting/objects/event-element-assl.md)|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[Miningstructurecolumn-Objekt](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Für **DrillThroughAction** -Elemente identifiziert die **Columns** -Auflistung die Spalten, die Daten enthalten, die beim Ausführen der Aktion zurückgegeben werden sollen.  
  
 Für **TableMiningStructureColumn** -Elemente lässt die **Columns** -Auflistung nur eine Ebene der Rekursion zu. Mit anderen Worten, jedes **TableMiningStructureColumn** -Element in dieser Auflistung kann keine **TableMiningStructureColumn** -Elemente in seiner **Columns** -Auflistung enthalten.  
  
 Einige der entsprechenden Elemente im AMO-Objektmodell (Analysis Management Objects) sind <xref:Microsoft.AnalysisServices.TraceColumnCollection>, <xref:Microsoft.AnalysisServices.MiningModelColumnCollection> und <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
