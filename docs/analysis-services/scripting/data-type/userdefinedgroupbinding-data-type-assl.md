---
title: UserDefinedGroupBinding-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: UserDefinedGroupBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: UserDefinedGroupBinding
helpviewer_keywords: UserDefinedGroupBinding data type
ms.assetid: 70149929-0ff7-4a67-84bf-e94908ae7611
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 606bb4381a11fbda9a820176030fdd9b73439db3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="userdefinedgroupbinding-data-type-assl"></a>UserDefinedGroupBinding-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert einen abgeleiteten Datentyp, der eine benutzerdefinierte Gruppierung für ein Attribut darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<UserDefinedGroupBinding>  
   <!-- The following elements extend Binding -->  
      <AttributeID>...</AttributeID>  
      <Groups>...</Groups>  
</UserDefinedGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[Bindung](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [Gruppen](../../../analysis-services/scripting/collections/groups-element-assl.md)|  
|Abgeleitete Elemente|Finden Sie unter [binden](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 **UserDefinedGroupBinding** automatisch so behandelt, als ein [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), deren [Typ](../../../analysis-services/scripting/properties/type-element-binding-assl.md) -Elementgruppe ist *alle*.  
  
 Weitere Informationen zu den **binden** Typs, einschließlich der Tabellen von Analysis Services Scripting Language (ASSL) von Objekten des der **binden** Typ und der Vererbungshierarchie der **binden**  , finden Sie unter [Binding-Datentyp &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Einen Überblick über datenbindungen in ASSL finden Sie unter [&#40; Datenquellen und Bindungen SSAS – mehrdimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
