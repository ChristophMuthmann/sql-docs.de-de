---
title: DrillThroughAction-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DrillThroughAction Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DrillThroughAction
helpviewer_keywords: DrillThroughAction data type
ms.assetid: e212d575-a0d7-4548-92b4-33542ef59034
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 27314fccdc2b91cbba5ea70d793058c522ef015b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="drillthroughaction-data-type-assl"></a>DrillThroughAction-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert einen abgeleiteten Datentyp, der eine Drillthrough-Aktion darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DrillThroughAction>  
   <!-- The following elements extend Action -->  
   <Default>...</Default>  
   <Columns>...</Columns>  
</DrillThroughAction>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[Aktion](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Spalten](../../../analysis-services/scripting/collections/columns-element-assl.md), [Standard](../../../analysis-services/scripting/properties/default-element-assl.md)|  
|Abgeleitete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) ([Aktionen](../../../analysis-services/scripting/collections/actions-element-assl.md), Auflistung von [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), oder [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.DrillThroughAction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
