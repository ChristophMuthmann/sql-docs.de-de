---
title: AggregateFunction-Element (ASSL) | Microsoft Docs
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
- AggregateFunction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregateFunction
helpviewer_keywords:
- AggregateFunction element
ms.assetid: 880b6bd0-d62a-4221-831c-39f748ee84f2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c7e713cb8ac1a6bc27bca0cc23f7f4e191850f40
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="aggregatefunction-element-assl"></a>AggregateFunction-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert den Typ der Aggregatfunktion, die verwendet werden, indem eine [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Sum*|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Measure](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Sum*|Das Measure wird mit der **Sum** -Funktion aggregiert.|  
|*Count*|Das Measure wird mit der **Count** -Funktion aggregiert.|  
|*Min*|Das Measure wird mit der **Min** -Funktion aggregiert.|  
|*Max*|Das Measure wird mit der **Max** -Funktion aggregiert.|  
|*DistinctCount*|Das Measure wird mit der **DistinctCount** -Funktion aggregiert.|  
|*InclusionThresholdSetting*|Das Measure wird nicht aggregiert.|  
|*ByAccount*|Das Measure wird gemäß dem Konto aggregiert.|  
|*AverageOfChildren*|Das Measure wird durch Zurückgeben des Durchschnitts der untergeordneten Elemente aggregiert.|  
|*FirstChild*|Das Measure wird durch Zurückgeben des ersten untergeordneten Elements aggregiert.|  
|*LastChild*|Das Measure wird durch Zurückgeben des letzten untergeordneten Elements aggregiert.|  
|*FirstNonEmpty*|Das Measure wird durch Zurückgeben des ersten nicht leeren Elements aggregiert.|  
|*LastNonEmpty*|Das Measure wird durch Zurückgeben des letzten nicht leeren Elements aggregiert.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **AggregateFunction** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
