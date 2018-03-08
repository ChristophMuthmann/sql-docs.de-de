---
title: Usage-Element (MiningModelColumn) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Usage Element (MiningModelColumn)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Usage
helpviewer_keywords: Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a0e49b1156817f720b0c7db3205a8d1697ae6b8f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Usage-Element (MiningModelColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Beschreibt, wie die zugeordnete Spalte im übergeordneten [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|value|Description|  
|-----------|-----------------|  
|*Key*|Die Spalte ist eine Schlüsselspalte.|  
|*Eingabe*|Die Spalte ist eine Eingabespalte.|  
|*Predict*|Die Spalte ist eine Vorhersagespalte.|  
|*PredictOnly*|Die Spalte ist nur eine Vorhersagespalte.|  
|*Keine*|Die Spalte wird nicht vom Modell verwendet.<br /><br /> **\*\*Warnung \* \***  , wenn der Wert der Auslastung des "None" ist, Analysis Services sendet keine ausnahmslos an den Server in der Standardeinstellung; daher wird das Usage-Attribut nicht in der Anforderung/Antwort enthalten.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **Verwendung** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
