---
title: DiscretizationBucketCount-Element (ASSL) | Microsoft Docs
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
- DiscretizationBucketCount Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DiscretizationBucketCount
helpviewer_keywords:
- DiscretizationBucketCount element
ms.assetid: 551a73ae-59e1-4079-a2d9-988df96b5e07
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a9beb1b2930004786c4342836af5f39cbc7c314f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="discretizationbucketcount-element-assl"></a>DiscretizationBucketCount-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält die Anzahl der Buckets, in denen diskretisiert werden soll.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Integer|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert des **DiscretizationBucketCount** -Elements bestimmt, wie viele Gruppen oder "Buckets" erstellt werden, wenn Werte für **DimensionAttribute** oder **ScalarMiningStructureColumn** diskretisiert oder in einer spezifischen Menge an Gruppen angeordnet werden. Wenn das Element nicht angegeben wird, oder 0 (null) für den Wert des Elements angegeben ist [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] erstellt eine geeignete Anzahl an Gruppen in Abhängigkeit von der Diskretisierungsmethode. Weitere Informationen über die Diskretisierung finden Sie unter [Diskretisierungsmethoden &#40;Data Mining&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **DiscretizationBucketCount** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.DimensionAttribute> und <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Siehe auch  
 [DiscretizationMethod-Element &#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
