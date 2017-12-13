---
title: IsDefaultMeasure-Element (XML) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 523cf3d7-9df0-4f9d-8486-9109de8d3cca
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f904c9185c98adc0965f735bbd4e36e0aa93ae12
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="isdefaultmeasure-element-xml"></a>IsDefaultMeasure-Element (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Gibt an, dass es möglich ist, das Standardmeasure für diese Entität durch Navigieren von dieser Beziehung zur anderen Tabelle abrufen und Abrufen des Members mit das Attribut, DefaultMeasure.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|false|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Für **RelationshipEndVisualizationProperties** -Elemente gibt das **IsDefaultMeasure** -Element an, dass das Standardmeasure für diese Entität durch Navigieren zum anderen Ende der Beziehung abgerufen werden kann. Der Standardwert **false** gibt an, dass kein abzurufendes Standardmeasure vorhanden ist.  
  
  
