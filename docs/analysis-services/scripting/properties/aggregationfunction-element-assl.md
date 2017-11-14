---
title: AggregationFunction-Element (ASSL) | Microsoft Docs
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
apiname:
- AggregationFunction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationFunction
helpviewer_keywords:
- AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e14f744b35fc1d48ba2a96b15bd8bc3ec46e8e20
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationfunction-element-assl"></a>AggregationFunction-Element (ASSL)
  Enthält die Aggregationsfunktion, die für den Kontotyp zu verwenden ist.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Sum*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Konto](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der folgenden Zeichenfolgen beschränkt:  
  
|Wert|Description|  
|-----------|-----------------|  
|*Sum*|Das Measure wird mit der **Sum** -Funktion aggregiert.|  
|*Anzahl*|Das Measure wird mit der **Count** -Funktion aggregiert.|  
|*Min*|Das Measure wird mit der **Min** -Funktion aggregiert.|  
|*Max*|Das Measure wird mit der **Max** -Funktion aggregiert.|  
|*DistinctCount*|Das Measure wird mit der **DistinctCount** -Funktion aggregiert.|  
|*Keine*|Das Measure wird nicht aggregiert.|  
|*AverageOfChildren*|Das Measure wird durch Zurückgeben des Durchschnitts der untergeordneten Elemente aggregiert.|  
|*FirstChild*|Das Measure wird durch Zurückgeben des ersten untergeordneten Elements aggregiert.|  
|*LastChild*|Das Measure wird durch Zurückgeben des letzten untergeordneten Elements aggregiert.|  
|*FirstNonEmpty*|Das Measure wird durch Zurückgeben des ersten nicht leeren Elements aggregiert.|  
|*LastNonEmpty*|Das Measure wird durch Zurückgeben des letzten nicht leeren Elements aggregiert.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **AggregationFunction** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Accounts-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

