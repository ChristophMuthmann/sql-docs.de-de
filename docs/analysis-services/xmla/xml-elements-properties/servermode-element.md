---
title: ServerMode-Element | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c0d0def053cf923474f8d8d3cd066a87bdc31833
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="servermode-element"></a>ServerMode-Element
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Die **ServerMode** -Serverelement gibt den Modus an, in der Server betrieben wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|(none)|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Der Server arbeitet in einem der folgenden beiden Modi:  
  
|value|Description|  
|-----------|-----------------|  
|*Mehrdimensionale*|Mehrdimensionaler und Data Mining-Modus|  
|*Tabellarische*|Tabellenmodus|  
|*SharePoint*|SharePoint-Modus|  
  
## <a name="see-also"></a>Siehe auch  
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  
