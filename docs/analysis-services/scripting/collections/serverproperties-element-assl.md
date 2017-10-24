---
title: ServerProperties-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ServerProperties Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ServerProperties
helpviewer_keywords:
- ServerProperties element
ms.assetid: 8ccbef3f-1388-4fa3-b0a4-c89b89f09056
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19cb54012e1c78afc87095f1e7b221c66edac4e1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="serverproperties-element-assl"></a>ServerProperties-Element (ASSL)
  Enthält die Auflistung der [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) Elemente, die zu einem [Server](../../../analysis-services/scripting/objects/server-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Server>  
      ...  
   <ServerProperties>  
      <ServerProperty>...</ServerProperty>  
   </ServerProperties>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Untergeordnete Elemente|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.ServerPropertyCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

