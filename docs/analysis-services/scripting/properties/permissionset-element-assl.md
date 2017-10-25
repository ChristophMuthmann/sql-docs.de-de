---
title: PermissionsSet-Element (ASSL) | Microsoft Docs
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
- PermissionSet Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1448c3db59f149697fa429e6d122d9d20fd403f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="permissionset-element-assl"></a>PermissionsSet-Element (ASSL)
  Identifiziert den zugeordneten Berechtigungssatz eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Assembly.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Safe*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Safe*|Nur interne Berechnung und lokaler Datenzugriff werden ermöglicht. *Safe* ist der restriktivste Berechtigungssatz. Code, der von einer Assembly mit *Safe* -Berechtigungen ausgeführt wird, hat keinen Zugriff auf externe Systemressourcen wie Dateien, das Netzwerk, Umgebungsvariablen oder die Registrierung.|  
|*"ExternalAccess"*|*Safe*, mit der zusätzlichen Fähigkeit, auf externe Systemressourcen wie Dateien, Netzwerke, Webdienste, Umgebungsvariablen und die Registrierung zuzugreifen.|  
|*Nicht eingeschränkt*|Uneingeschränkte ermöglicht Assemblys den uneingeschränkten Zugriff auf Ressourcen sowohl innerhalb als auch außerhalb [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Code, der innerhalb einer *Unrestricted* -Assembly ausgeführt wird, kann nicht verwalteten Code aufrufen.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **PermissionSet** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.PermissionSet>.  
  
## <a name="see-also"></a>Siehe auch  
 [ComAssembly-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Assemblies-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Database-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Server-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

