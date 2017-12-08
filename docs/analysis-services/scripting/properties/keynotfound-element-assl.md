---
title: KeyNotFound-Element (ASSL) | Microsoft Docs
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
apiname: KeyNotFound Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyNotFound
helpviewer_keywords: KeyNotFound element
ms.assetid: 2a93bbfa-2409-4e94-8b68-926532895a4c
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 72ebb26afc343b771e32087e9d68f4978cdaedc8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="keynotfound-element-assl"></a>KeyNotFound-Element (ASSL)
  Gibt an, wie [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] reagiert, wenn einen Fehler der referenziellen Integrität festgestellt wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyNotFound>...</KeyNotFound>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*ReportAndContinue*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Fehler in der referenziellen Integrität treten auf, wenn ein Fremdschlüsselwert in einer abhängigen Tabelle keinen entsprechenden Eintrag in der übergeordneten Tabelle aufweist. Dieser Fehler tritt auf, wenn [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verarbeitet eine Dimension, die in der die Faktentabelle verweist auf einen Fremdschlüsselwert, der in der Dimensionstabelle für diese Dimension nicht vorhanden ist oder wenn [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] der Dimension Main Tabelle für eine Partition verarbeitet ein Dimension, in der Partition enthalten ist, verweist auf ein Schlüssel-Wert, der nicht in weiteren zugeordneten Dimensionstabelle existiert. (Bei Dimensionen mit Über-/Unterordnungshierarchien und übergeordneten Attributen kann der Fehler auch dann auftreten, wenn die Dimensionshaupttabelle für eine Dimension, die in der Partition enthalten ist, auf einen Schlüsselwert verweist, der nicht in derselben Dimensionstabelle existiert.)  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*IgnoreError*|Die Verarbeitung sollte den Fehler ignorieren und fortfahren.|  
|*ReportAndContinue*|Die Verarbeitung sollte den Fehler berichten und fortfahren.|  
|*ReportAndStop*|Die Verarbeitung sollte den Fehler berichten und anhalten.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **KeyNotFound** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
