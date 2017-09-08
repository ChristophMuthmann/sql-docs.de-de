---
title: StandardAction-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- StandardAction Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- StandardAction
helpviewer_keywords:
- StandardAction data type
ms.assetid: 81b574d5-06c1-4587-8bd2-0e5c5e3b1d99
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d57cf9ec56c160d49111b3301f11dbed72e383a1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="standardaction-data-type-assl"></a>StandardAction-Datentyp (ASSL)
  Definiert einen abgeleiteten Datentyp, der eine stellt [Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) Element außer einer [DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md) Element oder ein [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<StandardAction>  
   <!-- The following elements extend Action -->  
   <Expression>...</Expression>  
</StandardAction>  
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
|Untergeordnete Elemente|[Ausdruck](../../../analysis-services/scripting/properties/expression-element-assl.md)|  
|Abgeleitete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) ([Aktionen](../../../analysis-services/scripting/collections/actions-element-assl.md) Auflistung von [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) oder [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
