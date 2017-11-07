---
title: Roles-Element (ASSL) | Microsoft Docs
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
- Roles Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3c077f05af1af38b2160d07bedf3e6ae401acd0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="roles-element-assl"></a>Roles-Element (ASSL)
  Enthält die Auflistung der [Role](../../../analysis-services/scripting/objects/role-element-assl.md) -Elemente, die unter dem übergeordneten Element definiert sind.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
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
|Übergeordnete Elemente|[Database](../../../analysis-services/scripting/objects/database-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Untergeordnete Elemente|[Rolle](../../../analysis-services/scripting/objects/role-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das **Roles** -Element, das einem **Server** -Element zugeordnet ist, enthält nur eine Rolle mit dem Namen Administrators, die die Serveradministratorrolle darstellt. Die Serveradministratorrolle kann nicht geändert oder gelöscht werden. Ein Hinzufügen zusätzlicher Rollen zur Auflistung ist ebenfalls nicht möglich.  
  
 Das **Roles** -Element, das einem **Database** -Element zugeordnet ist, enthält die für diese Datenbank definierten Rollen.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.RoleCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

