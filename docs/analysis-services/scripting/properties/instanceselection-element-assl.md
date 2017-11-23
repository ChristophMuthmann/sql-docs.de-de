---
title: InstanceSelection-Element (ASSL) | Microsoft Docs
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
apiname: InstanceSelection Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd380986bf21d773dc9726b17eff816bf45af0ec
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="instanceselection-element-assl"></a>InstanceSelection-Element (ASSL)
  Stellt einen Hinweis für Clientanwendungen bezüglich der Anzeige einer Liste von Elementen bereit, der auf der erwarteten Anzahl von Elementen in der Liste basiert.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Keine*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der folgenden Zeichenfolgen beschränkt:  
  
|Wert|Description|  
|-----------|-----------------|  
|*Keine*|Keine Auswahlliste anzeigen. Ermöglicht es den Benutzern, Werte direkt einzugeben.|  
|*Dropdownliste*|Die Anzahl der Elemente ist klein genug für die Anzeige in einer Dropdownliste.|  
|*Listee*|Die Anzahl der Elemente ist zu groß für eine Dropdownliste, erfordert aber keine Filter.|  
|*FilteredList*|Die Anzahl der Elemente ist groß genug, dass das Anwenden von Filtern für ihre Anzeige sinnvoll ist.|  
|*MandatoryFilter*|Die Anzahl der Elemente ist so groß, dass die Anzeige immer gefiltert werden muss.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **InstanceSelection** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.InstanceSelection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
