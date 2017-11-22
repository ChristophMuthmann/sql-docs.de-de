---
title: Server-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: Server Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: server
helpviewer_keywords: Server element
ms.assetid: 92ca67f6-817e-4a75-9244-8f8bcf412190
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 12b6eb44f2ef433657f7252f10059df892cb71cc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="server-element-assl"></a>Server-Element (ASSL)
  Beschreibt eine Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Server>  
   <!—These elements are common to each major object -->  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Annotations>...</Annotations>  
   <!-- server elements or properties -->  
   <ProductName>...</ProductName>  
   <Edition>...</Edition>  
   <EditionId>...</Edition>  
   <Version>...</Version>  
   <ServerMode>...</ServerMode>  
   <ProductLevel>...</Databases>  
   <Databases>...</Databases>  
   <Assemblies>...</Assemblies>  
   <Traces>...</Traces>  
   <Roles>...</Roles>  
   <ServerProperties>...</ServerProperties>  
</Server>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Namen](../../../analysis-services/scripting/properties/name-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [Beschreibung](../../../analysis-services/scripting/properties/description-element-assl.md), [Anmerkungen ](../../../analysis-services/scripting/collections/annotations-element-assl.md), [ProductName](../../../analysis-services/scripting/properties/productname-element-assl.md), [Edition](../../../analysis-services/scripting/properties/edition-element-assl.md), [EditionId](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md), [Version](../../../analysis-services/scripting/properties/version-element-assl.md), [ServerMode](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md), [ProductLevel](../../../analysis-services/xmla/xml-elements-properties/productlabel-element.md), [Datenbanken](../../../analysis-services/scripting/collections/databases-element-assl.md), [Assemblys](../../../analysis-services/scripting/collections/assemblies-element-assl.md), [Ablaufverfolgungen](../../../analysis-services/scripting/collections/traces-element-assl.md), [Rollen](../../../analysis-services/scripting/collections/roles-element-assl.md), [ServerProperties](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>Hinweise  
 Das **Server** -Element stellt eine Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]dar und dient als oberster Knoten in der ASSL-Knotenhierarchie (Analysis Services Scripting Language).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Server>.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
