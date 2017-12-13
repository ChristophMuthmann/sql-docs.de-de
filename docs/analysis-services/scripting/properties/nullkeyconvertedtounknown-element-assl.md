---
title: NullKeyConvertedToUnknown-Element (ASSL) | Microsoft Docs
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
apiname: NullKeyConvertedToUnknown Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NullKeyConvertedToUnknown
helpviewer_keywords: NullKeyConvertedToUnknown element
ms.assetid: 1a6cde33-01ba-4095-b464-16d1ad3c6905
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: da985c222a0e5bb6fa36fe1ed0f102e7d79fa547
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="nullkeyconvertedtounknown-element-assl"></a>NullKeyConvertedToUnknown-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Gibt die Aktion, die beim Auftreten eines null-Konvertierungsfehlers ergriffen werden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*IgnoreError*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 NULL-Konvertierungsfehler treten auf, wenn ein Nullwert in einer Schlüsselspalte vorkommt und als **Unknown** -Element interpretiert wird. Dieser Fehler tritt jedoch nur, wenn die [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md) -Element für die [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) Vorgänger des der **ErrorConfiguration** übergeordnetes Element festgelegt ist, um  *UnknownMember*.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*IgnoreError*|Die Verarbeitung ignoriert den Fehler und setzt die Verarbeitung fort.|  
|*ReportAndContinue*|Die Verarbeitung meldet den Fehler und setzt die Verarbeitung fort.|  
|*ReportAndStop*|Die Verarbeitung meldet den Fehler und beendet die Verarbeitung.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **NullKeyConvertedToUnknown** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Siehe auch  
 [ErrorConfiguration-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
