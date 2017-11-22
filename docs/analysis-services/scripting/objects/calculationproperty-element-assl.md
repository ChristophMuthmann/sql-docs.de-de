---
title: CalculationProperty-Element (ASSL) | Microsoft Docs
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
apiname: CalculationProperty Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CalculationProperty
helpviewer_keywords: CalculationProperty element
ms.assetid: 5f0b4cfc-7d25-4c01-a517-cc2e89859be3
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f975a682331240400bbb9c215ca6596220d064c1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="calculationproperty-element-assl"></a>CalculationProperty-Element (ASSL)
  Enthält eine Auflistung von Benutzeroberflächeneigenschaften für eine Berechnung, die in verwendet ein [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CalculationProperties>  
   <CalculationProperty>  
      <CalculationReference>...</CalculationReference>  
      <CalculationType>...</CalculationType>  
      <Translations>...</Translations>  
      <Description>...</Description>  
      <Visible>...</Visible>  
      <SolveOrder>...</SolveOrder>  
      <FormatString>...</FormatString>  
      <ForeColor>...</ForeColor>  
      <BackColor>...</BackColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <NonEmptyBehavior>...</NonEmptyBehavior>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <DisplayFolder>...</DisplayFolder>  
   </CalculationProperty>  
</CalculationProperties>  
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
|Übergeordnete Elemente|[CalculationProperties](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|  
|Untergeordnete Elemente|[AssociatedMeasureGroupID](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md), [BackColor](../../../analysis-services/scripting/properties/backcolor-element-assl.md), [CalculationReference](../../../analysis-services/scripting/properties/calculationreference-element-assl.md), [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md), [Beschreibung](../../../analysis-services/scripting/properties/description-element-assl.md), [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [FontFlags](../../../analysis-services/scripting/properties/fontflags-element-assl.md), [FontName](../../../analysis-services/scripting/properties/fontname-element-assl.md), [FontSize](../../../analysis-services/scripting/properties/fontsize-element-assl.md), [ForeColor](../../../analysis-services/scripting/properties/forecolor-element-assl.md), ["FormatString"](../../../analysis-services/scripting/properties/formatstring-element-assl.md), [NonEmptyBehavior](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md), [SolveOrder](../../../analysis-services/scripting/properties/solveorder-element-assl.md), [Übersetzungen](../../../analysis-services/scripting/collections/translations-element-assl.md), [sichtbar](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
