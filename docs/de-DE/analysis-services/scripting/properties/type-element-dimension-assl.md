---
title: Geben Sie-Element (Dimension) (ASSL) | Microsoft Docs
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
- Type Element (Dimension)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 075ebc645c67f496d7e6946035371244dd229c88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="type-element-dimension-assl"></a>Type-Element (Dimension) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Stellt Informationen über den Inhalt der Dimension bereit.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Regulär*|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Einige Werte für **Type**, beispielsweise *Accounts*, bestimmen spezifisches Verhalten.  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Regulär*|Die Dimension ist eine reguläre Dimension.|  
|*Zeit*|Die Dimension ist eine Zeitdimension.<br /><br /> Hinweis: Dieser Wert gibt an, dass die Dimension für Zeitdimensionen spezifische Funktionalität unterstützt.|  
|*Geography*|Die Dimension enthält geografische Attribute.|  
|*Organisation*|Die Dimension enthält Organisationsattribute.|  
|*BillOfMaterials*|Die Dimension enthält Stücklistenattribute.|  
|*Konten*|Die Dimension enthält kontobezogene Attribute.<br /><br /> Hinweis: Dieser Wert gibt an, dass die Dimension für kontodimensionen spezifische Funktionalität unterstützt.|  
|*Customers*|Die Dimension enthält kundenbezogene Attribute.|  
|*Produkte*|Die Dimension enthält produktbezogene Attribute.|  
|*Szenario*|Die Dimension enthält szenariobezogene Attribute.|  
|*Quantitative*|Die Dimension enthält quantitative Attribute.|  
|*Hilfsprogramm*|Die Dimension enthält Hilfsprogrammattribute.|  
|*Währung*|Die Dimension enthält Währungsattribute.|  
|*Raten*|Die Dimension enthält Wechselkursattribute.|  
|*Channel*|Die Dimension enthält Kanalattribute.|  
|*Promotion*|Die Dimension enthält höherstufungsbezogene Attribute.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **Typ** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DimensionType>.  
  
 Das Element, das das übergeordnete Element des entspricht **Typ** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
