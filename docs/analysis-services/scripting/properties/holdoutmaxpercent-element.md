---
title: HoldoutMaxPercent-Element | Microsoft Docs
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
f1_keywords: HoldoutMaxPercent
helpviewer_keywords: HoldoutMaxPercent element
ms.assetid: e375cc51-5f9d-4252-98a1-326ca0dbbf83
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4edfc8e9942dbbfd8408949ed03ee3de366c32dd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="holdoutmaxpercent-element"></a>HoldoutMaxPercent-Element
  Gibt den maximalen Prozentsatz von Fällen in der Datenquelle, die für die zurückhaltungspartition verwendet werden, die den Testsatz enthält eine [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) Element. Die übrigen Fälle werden zum Training verwendet. Ein Wert von 0 gibt an, dass die Anzahl der Fälle, die als Testsatz zurückgehalten werden können, unbegrenzt ist.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxPercent>...</ddl100_100:HoldoutMaxPercent>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Ganzzahl zwischen 0 und 99.|  
|Standardwert|30|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie sowohl für **HoldoutMaxPercent** als auch für **HoldoutMaxCases**Werte angeben, beschränkt der Algorithmus den Testsatz auf den kleineren der beiden Werte.  
  
 Ist für **HoldoutMaxCases** der Standardwert von 0 festgelegt, und wurde für **HoldoutMaxPercent**kein Wert definiert, verwendet der Algorithmus den gesamten Datensatz für das Training.  
  
 Die neuen Eigenschaften **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, oder **HoldoutActualSize** stehen nur in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und höheren Versionen. Deshalb müssen Sie diese Eigenschaften wie in der Syntaxbeschreibung gezeigt mit dem neuen Namespace als Präfix versehen, da [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] anderenfalls einen Fehler ausgibt.  
  
> [!NOTE]  
>  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] hat nicht die Verwendung von zurückhaltungspartitionen für Miningstrukturen unterstützt. Aus diesem Grund [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language (ASSL)-Anweisungen, die einen der zurückhaltungsparameter enthalten **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, oder **HoldoutActualSize**, kann nicht verwendet werden, [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Wenn Sie einen dieser zurückhaltungsparameter in einer ASSL-Anweisung in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] einen Fehler zurück.  
  
 Das Element, das das übergeordnete Element des entspricht **HoldoutMaxPercent** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxCases-Element](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)   
 [HoldoutSeed-Element](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [HoldoutActualSize-Element](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
