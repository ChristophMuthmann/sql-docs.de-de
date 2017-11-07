---
title: ProactiveCachingInheritedBinding-Datentyp (ASSL) | Microsoft Docs
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
- ProactiveCachingInheritedBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProactiveCachingInheritedBinding data type
ms.assetid: 913fa19f-1ecb-4fca-897e-12f0fb02cf8b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8692a0fc3f714f9654d3e4aabd85e0617b0dcee2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="proactivecachinginheritedbinding-data-type-assl"></a>ProactiveCachingInheritedBinding-Datentyp (ASSL)
  Definiert einen abgeleiteten Datentyp, die Informationen darstellt, die die [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) -Element über datenquellenänderungen in Tabellen und Sichten, die über vorhandene datenbindungen, das Neuerstellen des Caches erfordern, identifiziert.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ProactiveCachingInheritedBinding>  
   <!-- This element has no child elements that extend ProactiveCachingObjectNotificationBinding -->  
</ProactiveCachingInheritedBinding>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[ProactiveCachingObjectNotificationBinding](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|Keine|  
|Abgeleitete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen zu den **ProactiveCachingBinding** Typ, einschließlich einer Tabelle der Vererbungshierarchie der **ProactiveCachingBinding** , finden Sie unter [ProactiveCachingBinding-Daten Geben Sie &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md).  
  
 Weitere Informationen zu den **binden** Typs, einschließlich der Tabellen von Analysis Services Scripting Language (ASSL) von Objekten des der **binden** Typ und der Vererbungshierarchie der **binden**  , finden Sie unter [Binding-Datentyp &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Einen Überblick über datenbindungen in ASSL finden Sie unter [&#40; Datenquellen und Bindungen SSAS – mehrdimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.ProactiveCachingInheritedBinding>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

