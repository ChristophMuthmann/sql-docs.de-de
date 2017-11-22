---
title: FoldingParameters-Element (ASSL) | Microsoft Docs
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
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- FoldIndex
- FoldCount
- MaxCases
- FoldingParameters
- FoldTargetAttribute
helpviewer_keywords: FoldingParameters element
ms.assetid: 5f5c5a3e-4aed-48fb-bca5-e67f421bef2f
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8d6565a5898f5f41898d82a1d70d3748f8b2883c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="foldingparameters-element-assl"></a>FoldingParameters-Element (ASSL)
  Gibt an, die vom verwendeten Parameter den [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Server, wenn sie die übergreifende Überprüfung von Miningmodellen ausführt.  
  
> [!NOTE]  
>  Diese Parameter dienen nur zur internen Verwendung. Die hier bereitgestellten Informationen dienen lediglich als Referenz.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningModel>  
   ...  
   <ddl100_100:FoldingParameters>...  
      <ddl100_100:FoldIndex>...</ddl100_100:FoldIndex>  
      <ddl100_100:FoldCount>...</ddl100_100:FoldCount>  
      <ddl100_100:MaxCases>...</ddl100_100:MAxCases>  
      <ddl100_100:FoldTargetAttribute>...</ddl100_100:FoldTargetAttribute  
...</ddl100_100:FoldingParameters>  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|*FoldIndex*|Ganze Zahl, die die Anfangsposition der zur Kreuzvalidierung verwendeten Partition angibt.|  
|*FoldCount*|Ganze Zahl, die die Anzahl von Partitionen im Modell nach der Kreuzvalidierung angibt.|  
|*MaxCases*|Ganze Zahl, die angibt, wie viele Modellfälle zur Kreuzvalidierung verwendet werden.<br /><br /> Ein Wert von 0 gibt an, dass alle Fälle verwendet werden.|  
|*FoldTargetAttribute*|Zeichenfolge, die die ID der Modellsspalte angibt, die das vorhersagbare Attribut enthält.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Untergeordnete Elemente|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaften sind nur zur internen Verwendung, und werden nicht zur Verwendung in DDL-Anweisungen unterstützt.  
  
 Informationen zur Verwendung von kreuzvalidierung in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], finden Sie unter [Measures in der übergreifenden Überprüfungsbericht](../../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
 Informationen zum Ausführen der kreuzvalidierung mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] gespeicherte Prozeduren finden Sie unter [Data Mining gespeicherte Prozeduren &#40; Analysis Services – Datamining &#41; ](../../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
