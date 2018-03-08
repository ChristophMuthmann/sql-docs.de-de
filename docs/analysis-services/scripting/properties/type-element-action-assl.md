---
title: Geben Sie-Element (Action) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Type Element (Action)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TYPE
helpviewer_keywords: Type element
ms.assetid: 534cdf99-1edf-4490-9eaa-61f189a19434
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d7dffa090a3f8b24c08329f14f22881cf45d017b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="type-element-action-assl"></a>Type-Element (Action) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Enthält den Typ des der [Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|value|Description|  
|-----------|-----------------|  
|*URL*|Zeigt eine veränderliche Seite in einem Internetbrowser an.|  
|*HTML*|Führt ein HTML-Skript in einem Internetbrowser aus.|  
|*Anweisung*|Führt einen OLE DB-Befehl aus.|  
|*DrillThrough*|Ruft ein Rowset für Drillthrough ab.<br /><br /> Dieser Wert ist mit *Rowset* identisch und identifiziert Drillthroughaktionen. Er kann nur bei Aktionen verwendet, deren [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) Wert wird festgelegt, um *Zellen*.|  
|*DataSet*|Ruft ein Dataset ab.|  
|*Rowset*|Ruft ein Rowset ab.|  
|*Befehlszeile*|Führt einen Befehl an einer Eingabeaufforderung aus.|  
|*Proprietäre*|Führt eine Operation aus, wobei eine andere Schnittstelle als die in der Tabelle zuvor aufgeführten verwendet wird.|  
|*Bericht*|Zeigt eine veränderliche Seite in einem Internetbrowser an.<br /><br /> Dieser Wert ist mit *Url* identisch und identifiziert Berichtsaktionen.|  
  
 Das Element, das das übergeordnete Element des entspricht **Typ** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DrillThroughAction-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [ReportAction-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
