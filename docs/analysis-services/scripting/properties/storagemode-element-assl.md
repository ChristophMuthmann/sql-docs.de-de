---
title: StorageMode-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- StorageMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- StorageMode
helpviewer_keywords:
- StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6742eaff827086c8aac5d39e51dbf2e296c6b15d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="storagemode-element-assl"></a>StorageMode-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Bestimmt den Speichermodus für das übergeordnete Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*MOLAP*|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Cube-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md), [Dimension-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [Partition Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*MOLAP*|Das übergeordnete Element verwendet die mehrdimensionale OLAP (MOLAP)-Speicherung.|  
|*ROLAP*|Das übergeordnete Element verwendet die relationale OLAP (ROLAP)-Speicherung.|  
|*HOLAP*|Das übergeordnete Element verwendet die hybride OLAP (HOLAP)-Speicherung.<br /><br /> Hinweis: Dieser Wert gilt nicht für [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) übergeordneten Elementen.|  
|*InMemory*|Das übergeordnete Element verwendet IMBI-Speicher.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **StorageMode** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.StorageMode>.  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **StorageMode** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup>, und <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
