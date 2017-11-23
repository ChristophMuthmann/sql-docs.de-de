---
title: RefreshPolicy-Element (ASSL) | Microsoft Docs
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
apiname: RefreshPolicy Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RefreshPolicy
helpviewer_keywords: RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84fcc378f14364c5728e78fc9ee866ecca2dad8b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy-Element (ASSL)
  Bestimmt, wie oft im dynamischen Teil der Gruppe Dimension oder Measuregruppe (gemäß der [Persistenz](../../../analysis-services/scripting/properties/persistence-element-assl.md) Element) wird geprüft, ob Änderungen.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|Finden Sie in der folgenden Tabelle aus.|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
|Vorgänger oder übergeordnetes Element|Standardwert|  
|------------------------|-------------------|  
|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|Keine|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*ByQuery*|Jede Abfrage überprüft, ob sich die Quelldaten geändert haben.|  
|*ByInterval*|Quelldaten ist nur für Änderungen an der angegebenen Intervalls aktiviert ["RefreshInterval"](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md).|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **RefreshPolicy** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.RefreshPolicy>.  
  
## <a name="see-also"></a>Siehe auch  
 [Persistence-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
