---
title: Geben Sie-Element (Action) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
ms.openlocfilehash: 3a84623ef5ee2b870e767217ae5f8664ac44d517
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="type-element-action-assl"></a>Type-Element (Action) (ASSL)
  Enthält den Typ des der [Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
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
  
## <a name="see-also"></a>Siehe auch  
 [DrillThroughAction-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [ReportAction-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
