---
title: NullKeyNotAllowed-Element (ASSL) | Microsoft Docs
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
apiname: NullKeyNotAllowed Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: NullKeyNotAllowed
helpviewer_keywords: NullKeyNotAllowed element
ms.assetid: 4ece99eb-954b-4da1-add4-dd9efd5fff0a
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45ad433dc247749c466f05896a89bc25bee0680d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="nullkeynotallowed-element-assl"></a>NullKeyNotAllowed-Element (ASSL)
  Bestimmt, wie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Verarbeitungsmodul einen null-Schlüsselfehler während der Verarbeitung auftreten.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ErrorConfiguration>  
   ...  
   <NullKeyNotAllowed>...</NullKeyNotAllowed>  
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
 NULL-Schlüsselfehler treten auf, wenn ein NULL-Wert in einer Schlüsselspalte auftritt, in der NULL-Werte nicht zulässig sind, wodurch ein Verwerfen des Datensatzes während der Verarbeitung erzwungen wird. Dieser Fehler tritt jedoch nur, wenn die [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md) -Element für die **DataItem** Vorgänger des der **ErrorConfiguration** übergeordnetes Element festgelegt ist, um  *Fehler*.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*IgnoreError*|Die Verarbeitung ignoriert den Fehler und setzt die Verarbeitung fort.|  
|*ReportAndContinue*|Die Verarbeitung meldet den Fehler und setzt die Verarbeitung fort.|  
|*ReportAndStop*|Die Verarbeitung meldet den Fehler und beendet die Verarbeitung.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **NullKeyNotAllowed** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Siehe auch  
 [ErrorConfiguration-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
  
