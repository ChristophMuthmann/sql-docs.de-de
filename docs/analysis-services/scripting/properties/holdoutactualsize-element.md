---
title: HoldoutActualSize-Element | Microsoft Docs
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
f1_keywords: HoldoutActualSize
helpviewer_keywords: HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fc09419e2099c4e0cb5587c4d328ef876728584e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="holdoutactualsize-element"></a>HoldoutActualSize-Element
  Gibt die tatsächliche Größe an, nach der Verarbeitung der zurückhaltungspartition, die den Testsatz enthält eine [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) Element. Die übrigen Fälle im Datensatz werden zum Training verwendet. Diese Eigenschaft ist schreibgeschützt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Schreibgeschützter ganzzahliger Wert.|  
|Standardwert|Nicht zutreffend|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert für **HoldoutActualSize** hängt von den Quelldaten sowie von den Werten für [HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md), [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md), und [HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md). Daher ist der Wert für **HoldoutActualSize** ist erst verfügbar, nachdem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] die Miningstruktur verarbeitet.  
  
 Das Element, das das übergeordnete Element des entspricht **HoldoutActualSize** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
> [!NOTE]  
>  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] hat nicht die Verwendung von zurückhaltungspartitionen für Miningstrukturen unterstützt. Aus diesem Grund [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language (ASSL)-Anweisungen, die einen der zurückhaltungsparameter enthalten **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, oder **HoldoutActualSize**, kann nicht verwendet werden, [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Wenn Sie einen dieser zurückhaltungsparameter in einer ASSL-Anweisung in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] einen Fehler zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxCases-Element](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)   
 [HoldoutMaxPercent-Element](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutSeed-Element](../../../analysis-services/scripting/properties/holdoutseed-element.md)  
  
  
