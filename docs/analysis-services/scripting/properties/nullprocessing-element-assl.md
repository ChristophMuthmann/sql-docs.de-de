---
title: NullProcessing-Element (ASSL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- NullProcessing Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6faa6554c371cfaccb4ba6bd07772f0611816eeb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert, wie NULL-Werte verarbeitet werden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataItem>  
   ...  
   <NullProcessing>...</NullProcessing>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Automatic*|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Beibehalten*|Behält den NULL-Wert bei.<br /><br /> Hinweis: Dieser Wert wird für distinct Count Measures nicht unterstützt.|  
|*Fehler*|Löst einen NULL-Schlüsselfehler aus. Der Wert der [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md) bestimmt, wie die Instanz auf den Fehler reagiert.<br /><br /> Hinweis: Dieser Wert wird für Measures nicht unterstützt.|  
|*UnknownMember*|Generiert ein unbekanntes Element und löst einen NULL-Konvertierungsfehler aus. Der Wert der [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md) bestimmt, wie die Instanz auf den Fehler reagiert.<br /><br /> Hinweis: Dieser Wert wird für Measures gehörenden Spalten nicht unterstützt.|  
|*ZeroOrBlank*|Konvertiert den NULL-Wert zu 0 (für numerische Daten) oder in eine leere Zeichenfolge (für Daten in Zeichenfolge).<br /><br /> Hinweis: Dieser Wert stellt die Kompatibilität mit früheren Versionen von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Automatic*|Nutzt die für das Element geeignete Standardverarbeitung:<br /><br /> *ZeroOrBlank* für OLAP-Datenelemente.<br /><br /> *UnknownMember* für Data Mining-Datenelemente.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **NullProcessing** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.NullProcessing>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
