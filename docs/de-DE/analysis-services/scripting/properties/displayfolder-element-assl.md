---
title: DisplayFolder-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- DisplayFolder Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f5060ee7f1939c7e7dc4c04abf58a6d77f2c4abf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="displayfolder-element-assl"></a>DisplayFolder-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt den Ordner an, in dem das übergeordnete Element aufgelistet werden soll. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Anwendungen für Entwickler und Administratoren können die Verwendung von anzeigeordnern für die visuelle Kategorisierung mehrerer Elemente unterstützen.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md), [Übersetzung](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 In größeren Cubes gibt es möglicherweise Hunderte von Measures und Hierarchien. Die **DisplayFolder** -Eigenschaft definiert die Benutzerdarstellung auf dem Client. Der Wert der **DisplayFolder** -Eigenschaft kann eine der folgenden Optionen enthalten:  
  
-   Kann leer sein, wobei angegeben wird, dass das Measure nicht zu einem Ordner gehört.  
  
-   Kann einen einzelnen Ordnernamen enthalten, wobei angegeben wird, dass das Measure als zu einem Ordner mit diesem Namen gehörend gerendert werden sollte.  
  
-   Kann mehrere Ordnernamen getrennt durch einen umgekehrten Schrägstrich enthalten (\\), wobei eine eingebettete Ordnerhierarchie angegeben wird.  
  
 Die **DisplayFolder** Eigenschaft gilt für **CalculationProperty** Elemente, wenn der Wert der [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) auf festgelegt ist *Member* .  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **DisplayFolder** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.Measure>, und <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Siehe auch  
 [CalculationProperties-Element &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts-Element &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
