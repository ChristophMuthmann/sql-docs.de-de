---
title: MdxMissingMemberMode-Element (ASSL) | Microsoft Docs
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
- MdxMissingMemberMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MdxMissingMemberMode element
ms.assetid: aca6130b-5fb8-4fa1-af8b-8e1ef361926f
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2452957134b0c1118695e5a34565ca6053010eb8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdxmissingmembermode-element-assl"></a>MdxMissingMemberMode-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Legt die Verarbeitung fehlender Elemente in MDX-Anweisungen (Multidimensional Expressions) fest.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Dimension>  
   ...  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Standardwert*|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Dimension](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Ignorieren*|Fehlende Elemente werden ignoriert.|  
|*Fehler*|Ein Fehler wird ausgelöst, wenn fehlende Elemente gefunden werden.|  
|*Standardwert*|Fehlende Elemente werden ignoriert.|  
  
 Das Element, das das übergeordnete Element des entspricht **MdxMissingMemberMode** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionale Ausdrücke & #40; MDX & #41; Referenz](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
