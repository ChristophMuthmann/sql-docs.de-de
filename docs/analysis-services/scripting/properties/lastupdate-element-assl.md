---
title: LastUpdate-Element (ASSL) | Microsoft Docs
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
apiname: LastUpdate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: LastUpdate element
ms.assetid: 639db733-a082-4f57-868d-a3bcd5e7a4f6
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0137ecd5ec2344ece1c4ab65ad55ec344678e1bc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lastupdate-element-assl"></a>LastUpdate-Element (ASSL)
  Enthält einen schreibgeschützten Zeitstempel, der die letzte Zeitpunkt, den zugeordneten [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) oder jeglichen anderen Hauptobjekten, die die Datenbank enthält wurden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Database> <!-- or one of the elements that are listed in the Element Relationships table -->  
   ...  
   <LastUpdate>...</LastUpdate>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|DateTime|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die Elemente, die den übergeordneten Elementen von entsprechen **LastUpdate** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
