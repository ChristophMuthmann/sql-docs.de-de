---
title: Distribution-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Distribution Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Distribution
helpviewer_keywords:
- Distribution element
ms.assetid: a1309b90-8ad8-431b-a918-67f0cdd4fd20
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 20e87df47e6be29c91f4e9b47ac25b62506bc3b8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="distribution-element-assl"></a>Distribution-Element (ASSL)
  Enthält einen anbieterspezifischen Wert, der beschreibt, wie Skalare Werte innerhalb einer Spalte verteilt werden eine [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Distribution>...</Distribution>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die Werte, die für das **Distribution** -Element verfügbar sind (z. B. *Normal* oder *Uniform,* ) gelten speziell für jeden Mining-Algorithmusanbieter. Weitere Informationen über gültige **Distribution** -Werte finden Sie in der Mining-Algorithmusanbieter-Dokumentation.  
  
 Das übergeordnete Element des entsprechende Element **Verteilung** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

