---
title: SkippedLevelsColumn-Element (ASSL) | Microsoft Docs
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
- SkippedLevelsColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- SkippedLevelsColumn
helpviewer_keywords:
- SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 181e93110f5e482a04940ee5fe66bbba99b6c073
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="skippedlevelscolumn-element-assl"></a>SkippedLevelsColumn-Element (ASSL)
    
> [!NOTE]  
>  Diese Funktion wird in dieser Version von Microsoft SQL Server nicht mehr unterstützt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
 Stellt die Details einer Spalte bereit, die die Anzahl der übersprungenen (leeren) Ebenen zwischen den einzelnen Elementen und den jeweils übergeordneten Elementen speichert.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <SkippedLevelsColumn xsi:type="DataItem">...</SkippedLevelsColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die **SkippedLevelsColumn** Element gilt nur für übergeordnete Attribute (also der Wert der die [Verwendung](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) -Element für die **DimensionAttribute** übergeordneten festgelegt ist um *übergeordneten*). Das **SkippedLevelsColumn** -Element enthält die Spalte oder das Attribut für das übergeordnete Attribut, das die Anzahl übersprungener Ebenen zwischen jedem Element und dem übergeordneten Element speichert. Dies lässt Über-/Unterordnungshierarchien zu, die darauf basieren, dass übergeordnete Attribute Ebenen zwischen Elementen überspringen. Die in dieser Spalte oder diesem Attribut enthaltenen Werte müssen nicht negative ganze Zahlen sein. Andernfalls tritt ein Verarbeitungsfehler auf. Ist das **SkippedLevelsColumn** -Element nicht festgelegt oder enthält es keinen Wert, verfügt das aktuelle Element über eine Ebenentiefe, die eine Ebene geringer ist als die des übergeordneten Elements.  
  
 Weitere Informationen zu den **DataItem** Typ, einschließlich einer Tabelle von Analysis Services Scripting Language (ASSL)-Objekten und Eigenschaften von der **DataItem** table, finden Sie unter [DataItem-Datentyp &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Das Element, das das übergeordnete Element des entspricht **SkippedLevelsColumn** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Attributes-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Dimension-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
