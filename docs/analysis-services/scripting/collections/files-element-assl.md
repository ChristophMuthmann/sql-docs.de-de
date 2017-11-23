---
title: Element (ASSL)-Dateien | Microsoft Docs
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
apiname: Files Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Files
helpviewer_keywords: Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f7727da9a239596dfe0e6ffddd5e8bd783a3a64e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="files-element-assl"></a>Files-Element (ASSL)
  Enthält die Auflistung der [Datei](../../../analysis-services/scripting/objects/file-element-assl.md) Elemente, aus denen eine [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Assembly xsi:type="ClrAssembly">  
   ...  
   <Files>  
      <File xsi:type="ClrAssemblyFile">...</File>  
   </Files>  
   ...  
</Assembly>  
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
|Übergeordnete Elemente|[Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) des Typs [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|Untergeordnete Elemente|[Datei](../../../analysis-services/scripting/objects/file-element-assl.md) des Typs [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Server-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Database-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Assemblies-Element & #40; ASSL & #41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Data-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock-Datentyp & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks-Element & #40; ASSL & #41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly-Datentyp & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Schemaauflistungen & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
