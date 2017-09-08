---
title: Format-Element (ASSL) | Microsoft Docs
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
- Format Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb34b3f3f32492abb36a9f1bb6d645596493bfbc
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="format-element-assl"></a>Format-Element (ASSL)
  Enthält das erforderliche Format von der [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Zulässige Werte für das **Format** -Element sind Microsoft Office Excel-Formate und die Zeichenfolgen *TrimRight*, *TrimLeft*, *TrimAll*und *TrimNone*. Der Standardwert für Kürzungen ist *TrimRight* .  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|Eine beliebige Excel-Formatzeichenfolge|Daten werden gemäß der angegebenen benannten oder benutzerdefinierten Formatzeichenfolge formatiert. Es kann eine beliebige Formatzeichenfolge, die Excel unterstützt, bereitgestellt werden.|  
|*TrimAll*|Die Daten werden auf der linken und auf der rechten Seite gekürzt.|  
|*TrimLeft*|Die Daten werden auf der linken Seite gekürzt.|  
|*TrimNone*|Die Daten werden nicht gekürzt.|  
|*TrimRight*|Die Daten werden auf der rechten Seite gekürzt.|  
  
 Das Element, das das übergeordnete Element des entspricht **Format** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
