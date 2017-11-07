---
title: Password-Element (ASSL) | Microsoft Docs
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
- Password Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d83c0cccfaf1c4a50b2c10efead1f923012e6e0d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="password-element-assl"></a>Password-Element (ASSL)
  Enthält das Kennwort des Benutzerkontos für die [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Den Wert des der **Kennwort** Element als auch der Wert des der [Konto](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md) -Elements werden zum Zweck des Identitätswechsels verwendet, wenn der Wert des der [ImpersonationMode-Wert](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md) -Element für jedes Element abgeleitet aus der **ImpersonationInfo** Datentyp wird festgelegt, um *ImpersonateAccount*.  
  
 Nur Mitglieder der Rolle des Serveradministrators für die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz bieten einen leeren Wert für die **Kennwort** Element  
  
## <a name="see-also"></a>Siehe auch  
 [DataSourceImpersonationInfo-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

