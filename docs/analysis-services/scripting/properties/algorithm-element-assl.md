---
title: Algorithm-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Algorithm Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c73bc1f9a1b3a1cb7130cb52c5c8b199a9a3be8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="algorithm-element-assl"></a>Algorithm-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert den von einem [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) -Element verwendeten Algorithmus.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert, der die **Algorithmus** Element ist eine Zeichenfolge, die der Algorithmus identifiziert. Die Zeichenfolge kann z. B. *Microsoft_Naive_Bayes*, *Microsoft_Decision_Trees*, oder *Microsoft_Clustering.* Die Zeichenfolge identifiziert Algorithmen, die vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] und benutzerdefinierte Algorithmen, die vom Benutzer bereitgestellt werden. Verfügbare Werte für die **Algorithmus** Element abgerufen werden kann, aus der Spalte SERVICE_NAME des der [DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md) -Schemarowsets.  
  
 Das Element, das das übergeordnete Element des entspricht **Algorithmus** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MiningModel>. Ein eng verwandtes Element im AMO-Objektmodell ist <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>.  
  
## <a name="see-also"></a>Siehe auch  
 [AlgorithmParameter-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters-Element & #40; ASSL & #41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
