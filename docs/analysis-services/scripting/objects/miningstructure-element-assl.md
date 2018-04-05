---
title: MiningStructure-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MiningStructure Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 455d874cf279e44e8381c5183d2d376e40e2a351
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="miningstructure-element-assl"></a>MiningStructure-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert die Struktur für eine Reihe von Miningmodellen.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningStructures>  
   <MiningStructure>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <Source>...</Source>  
      <CreatedTimestamp>...</<CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <CacheMode>...</CacheMode>  
            <Columns>...</Columns>  
      <State>...</State>  
      <HoldoutActualSize>...</HoldoutActualSize>  
      <HoldoutMaxCases>...</HoldoutMaxCases>  
      <HoldoutMaxPercent>...</HoldoutMaxPercent>  
      <HoldoutSeed>...</HoldoutSeed>        
            <MiningStructurePermissions>...</<MiningStructurePermissions>  
            <MiningModels>...</MiningModels>  
            <Annotations>...</Annotations>  
   </MiningStructure>  
</MiningStructures>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|InclusionThresholdSetting|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[MiningStructures](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|  
|Untergeordnete Elemente|[Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), ["CacheMode"](../../../analysis-services/scripting/properties/cachemode-element-assl.md), [Sortierung](../../../analysis-services/scripting/properties/collation-element-assl.md), [Spalten](../../../analysis-services/scripting/collections/columns-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [ Beschreibung](../../../analysis-services/scripting/properties/description-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md),<br /><br /> [HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md),<br /><br /> [HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md),<br /><br /> [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md),<br /><br /> [HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md),<br /><br /> [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Sprache](../../../analysis-services/scripting/properties/language-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md), [ MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md), [Namen](../../../analysis-services/scripting/properties/name-element-assl.md), [Quelle](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Status](../../../analysis-services/scripting/properties/state-element-assl.md), [Übersetzungen](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Die Miningstruktur definiert die Spalten und die Bindungen. Nach dem Definieren einer Miningstruktur können Sie diese Struktur verwenden, um zahlreiche Miningmodelle zu definieren. Die Miningstruktur und jedes darin enthaltene Miningmodell können unabhängig voneinander verarbeitet werden.  
  
> [!NOTE]  
>  Die Holdout-Eigenschaften **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, und **HoldoutActualSize**, wurden in eingeführt [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Sie ermöglichen es Ihnen, eine Partition in einer Miningstruktur zu definieren, die als Testsatz für alle der Struktur zugeordneten Miningmodelle fungiert. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] unterstützt diese Eigenschaften nicht. Wenn Sie versuchen, diese Eigenschaften in einer Instanz von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] zu verwenden, gibt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] einen Fehler zurück.  
  
## <a name="drillthrough-to-structure-columns"></a>Drillthrough zu Strukturspalten  
 In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], ein neues Berechtigungselement hinzugefügt wurde die [MiningStructurePermissions-Element &#40; ASSL &#41; ](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) Auflistung. Wenn Sie hinzufügen **AllowDrillthrough** Berechtigung sowohl dem [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) und [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md) Auflistungen, Drillthrough aktiviert ist die Miningmodellinhalt in die Struktur so, dass Sie von einer Rolle mit Mitgliedern **AllowDrillthrough** Berechtigungen für das Modell können Datamining-Modell Abfragen und strukturspalten, die nicht im Modell enthalten waren zurückgeben.  
  
 Aus diesem Grund zum Schutz sensibler oder persönlicher Informationen sollten, erstellen Sie die Datenquellensicht so einrichten, dass vertraulichen Informationen, und **AllowDrillthrough** -Berechtigung für eine Miningstruktur nur bei Bedarf. Weitere Informationen finden Sie unter [AllowDrillThrough-Element &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Siehe auch  
 [MiningModel-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)   
 [SELECT &#40; DMX &#41;](../../../dmx/select-dmx.md)  
  
  
