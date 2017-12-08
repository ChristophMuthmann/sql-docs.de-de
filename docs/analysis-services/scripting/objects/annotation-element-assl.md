---
title: Annotation-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Annotation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Annotation
helpviewer_keywords: Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9583acd747910621f79622383f9eda6232dff5e2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="annotation-element-assl"></a>Annotation-Element (ASSL)
  Enthält Elemente, die verwendet werden, um das ASSL-Schema (Analysis Services Scripting Language) zu erweitern.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|Untergeordnete Elemente|[Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Value](../../../analysis-services/scripting/properties/value-element-assl.md), [Visibility](../../../analysis-services/scripting/properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das **Annotation** -Element bietet Erweiterbarkeit des ASSL-Schemas für alle Objekte, ausgenommen derer, die einzig zur Definition eines komplexen Datentyps verwendet werden. Das **Value** -Element des **Annotation** -Elements kann gemäß den folgenden Regeln gültiges XML aus allen XML-Namespaces enthalten, ausgenommen ASSL:  
  
-   XML kann nur Elemente enthalten.  
  
-   Jedes Element muss einen eindeutigen Namen haben. Es wird empfohlen, dass der Wert des **Name** -Elements des **Annotation** -Elements auf den Zielnamespace verweist.  
  
 Diese Regeln werden auferlegt, damit die Inhalte des **Annotation** -Elements als Menge von Name/Wert-Paaren über andere Schnittstellen, wie Decision Support Objects (DSO), verfügbar gemacht werden können.  
  
 Kommentare und Leerzeichen innerhalb des **Annotation** -Elements, die nicht in einem untergeordneten Element eingeschlossen sind, können nicht beibehalten werden. Außerdem müssen alle Elemente über Lese-/Schreibzugriff verfügen. Schreibgeschützte Elemente werden ignoriert.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Annotation>.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
