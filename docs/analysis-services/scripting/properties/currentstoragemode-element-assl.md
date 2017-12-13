---
title: CurrentStorageMode-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CurrentStorageMode Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CurrentStorageMode
helpviewer_keywords: CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f9f986a3a1f7d503896ae8fdf81a3a7329952b1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Bestimmt den aktuellen Speichermodus für das übergeordnete Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*ROLAP*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md), [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **CurrentStorageMode** -Element gibt den Speichermodus an, der derzeit für proaktives Zwischenspeichern verwendet wird, und gilt für alle Attribute des übergeordneten Elements.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*MOLAP*|Das übergeordnete Element verwendet die mehrdimensionale OLAP (MOLAP)-Speicherung.|  
|*ROLAP*|Das übergeordnete Element verwendet die relationale OLAP (ROLAP)-Speicherung.|  
|*HOLAP*|Das übergeordnete Element verwendet die hybride OLAP (HOLAP)-Speicherung.<br /><br /> Hinweis: Dieser Wert ist nur gültig für [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md) übergeordneten Elementen.|  
  
 Die Enumeration, die den zulässigen Werten entspricht **CurrentStorageMode** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.StorageMode>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
