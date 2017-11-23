---
title: Administer-Element (ASSL) | Microsoft Docs
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
apiname: Administer Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Administer
helpviewer_keywords: Administer element
ms.assetid: 52924cd6-6176-47c8-ab17-4ee0e0ce42b1
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: de42ea2bc2782f03aa31b875f8a6a6c3758dcb12
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="administer-element-assl"></a>Administer-Element (ASSL)
  Gibt an, ob die zugeordnete Berechtigung das Recht zur Verwaltung umfasst eine [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DatabasePermission>  
      ...  
      <Administer>...</Administer>  
   ...  
</DatabasePermission>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|False|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **Administer** -Element gibt an, ob ein Benutzer Verwaltungsfunktionen nur auf der angegebenen Datenbank ausführen kann. Die Serveradministratorrolle kann Verwaltungsfunktionen auf allen von der Instanz enthaltenen Datenbanken ausführen.  
  
 Das Element, das das übergeordnete Element des entspricht **verwalten** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Siehe auch  
 [Permission-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [Role-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
