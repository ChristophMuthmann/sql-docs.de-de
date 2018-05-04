---
title: NamingTemplateTranslation-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- NamingTemplateTranslation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NamingTemplateTranslation
helpviewer_keywords:
- NamingTemplateTranslation element
ms.assetid: 4a97a31d-23bc-4afd-a4dc-bc0ad7121f08
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 525b428d02f932858b4b7c4f30eb795a3e81abc6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="namingtemplatetranslation-element-assl"></a>NamingTemplateTranslation-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Stellt eine lokalisierte Übersetzung der [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md) -Element eines übergeordneten [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) -Datentyp.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<NamingTemplateTranslations>  
   <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
</NamingTemplateTranslations>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|[Übersetzung](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Namingtemplatetranslation](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Den Wert des der **NamingTemplateTranslation** Element wird nur von übergeordneten Attributen verwendet (also der Wert der der [Verwendung](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) Element von der **DimensionAttribute** übergeordnete festgelegt ist, um *übergeordneten*) zum Speichern der lokalisierten Übersetzung der **NamingTemplate** Wert für eine bestimmte Sprache.  
  
 Das Element, das das übergeordnete Element des entspricht **Namingtemplatetranslation** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [NamingTemplate-Element &#40;ASSL&#41;](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)   
 [Objekte & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
