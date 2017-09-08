---
title: ImpersonationMode-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ImpersonationMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ImpersonateMode
helpviewer_keywords:
- ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92091cdbdb14462629c18cc065f780b24d97b057
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="impersonationmode-element-assl"></a>ImpersonationMode-Element (ASSL)
  Enthält einen Wert, der die Methode des Identitätswechsels für Elemente, die angibt von der abgeleiteten der [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) -Datentyp.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Standardwert*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Standardwert*|Das übergeordnete Element verwendet die Identitätswechselmethode, die für den Kontext, in dem der Identitätswechsel verwendet wird, geeignet ist.|  
|*ImpersonateAccount*|Das übergeordnete Element verwendet die Anmeldeinformationen des Benutzerkontos, das im übergeordneten Element angegeben ist.|  
|*ImpersonateAnonymous*|Das übergeordnete Element verwendet die Anmeldeinformationen eines anonymen Benutzers.|  
|*ImpersonateCurrentUser*|Das übergeordnete Element verwendet die Anmeldeinformationen des aktuellen Benutzers.|  
|*Konfiguriert ImpersonateServiceAccount*|Das übergeordnete Element verwendet die Anmeldeinformationen des Dienstkontos, das mit der Instanz verknüpft ist [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **ImpersonationMode** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ImpersonationLevel>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
