---
title: Verfolgt-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- Traces Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Traces
helpviewer_keywords:
- Traces element
ms.assetid: 7ca2c7d1-fda3-4c76-9e32-fd9b5dda56e9
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0c33fc1188399987e46a9c739fcc5a031807b6ec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="traces-element-assl"></a>Traces-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält die Auflistung der [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) -Elemente, die zu einem [Server](../../../analysis-services/scripting/objects/server-element-assl.md) -Element gehören.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Server>  
      ...  
   <Traces>  
      <Trace>...</Trace>  
   </Traces>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Untergeordnete Elemente|[Trace](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.TraceCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
