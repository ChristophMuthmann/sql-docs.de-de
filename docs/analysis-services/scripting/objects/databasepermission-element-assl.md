---
title: DatabasePermission-Element (ASSL) | Microsoft Docs
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
- DatabasePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33711fc326cf8256cc9c641c047c90a1686505a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="databasepermission-element-assl"></a>DatabasePermission-Element (ASSL)
  Definiert die Standardberechtigungen in einem [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) -Element für ein bestimmtes [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DatabasePermissions>  
      <DatabasePermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <Administer>...</Administer>  
...</DatabasePermission>  
</DatabasePermissions>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|[Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Standardwert|False|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|  
|Untergeordnete Elemente|[Verwalten](../../../analysis-services/scripting/properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 **DatabasePermission** -Objekte können nur für Rollen vorhanden sein, die im Besitz der Datenbank sind, und nur ein **DatabasePermission** -Objekt kann für eine Rolle vorhanden sein.  
  
 Dieses Element verfügt über die folgenden Überprüfungen unter dem DeploymentMode-Wert 2 (tabellarisches Modell).  
  
-   *Administer* -Attribut, dessen Standardwert auf **False**festgelegt wird, außer wenn der Benutzer Administratorrechte besitzt. Für Benutzer mit Administratorrechten wird der Attributwert auf **True**festgelegt.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Siehe auch  
 [Role-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

