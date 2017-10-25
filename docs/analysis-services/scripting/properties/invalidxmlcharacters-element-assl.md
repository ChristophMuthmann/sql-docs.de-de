---
title: InvalidXmlCharacters-Element (ASSL) | Microsoft Docs
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
- InvalidXmlCharacters Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- InvalidXmlCharacters
helpviewer_keywords:
- InvalidXmlCharacters element
ms.assetid: 92b1210c-1075-4f2f-a2c4-dfdc6d7e5c05
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 76ee1ccf33324510f18d79229684310cc67cde25
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="invalidxmlcharacters-element-assl"></a>InvalidXmlCharacters-Element (ASSL)
  Gibt die Behandlungsmethode für ungültige XML-Zeichen in den Quelldaten an.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataItem>  
   ...  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
   ...  
</DataItem  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Beibehalten*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Beibehalten*|Ungültige XML-Zeichen werden beibehalten.|  
|*Entfernen*|Ungültige XML-Zeichen werden gelöscht.|  
|*Ersetzen*|Ungültige XML-Zeichen werden durch Fragezeichen (?) ersetzt.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **InvalidXmlCharacters** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.InvalidXmlCharacters>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

