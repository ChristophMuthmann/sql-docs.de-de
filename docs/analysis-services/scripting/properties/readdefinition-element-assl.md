---
title: ReadDefinition-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ReadDefinition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReadDefinition
helpviewer_keywords:
- ReadDefinition element
ms.assetid: 1f250129-13b2-41b9-b083-b5aacddf0060
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: afa07f4452bb7815ae30f2be3e8cccab6319eb9e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="readdefinition-element-assl"></a>ReadDefinition-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Bestimmt, ob Elemente die Datenbankdefinition oder die Definition der Objekte in der Datenbank lesen können.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Permission> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <ReadDefinition>...</ReadDefinition>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Keine*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md), [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [miningstructurepermission-Objekte ](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md), [Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|value|Description|  
|-----------|-----------------|  
|*Keine*|Der Zugriff auf die Objektdefinition ist nicht zulässig.|  
|*Grundlegende*|Der grundlegende Zugriff auf die Objektdefinition ist nicht zulässig.<br /><br /> Hinweis: Durch diese Berechtigung ist für lokale Cubes erstellen, verknüpfen Measuregruppen und Verknüpfen von Dimensionen erforderlich.|  
|*Zulässig*|Der vollständige Zugriff auf die Objektdefinition ist nicht zulässig.<br /><br /> Hinweis: Diese Berechtigung ist erforderlich für das Ausführen einer [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) XML for Analysis (XMLA) aufrufen, die mit dem DISCOVER_XML_METADATA-Parameter.|  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen **ReadDefinition** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission>, und <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Role-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
