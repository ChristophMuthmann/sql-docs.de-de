---
title: CellInfo-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CellInfo Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3a7b38201d5ba5c051cfacfb139ea52a6b93fb09
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="cellinfo-element-xmla"></a>CellInfo-Element (XMLA)
  Stellt die Zellmetadaten dar, die das übergeordnete [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) -Element enthält.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<OlapInfo>  
   ...  
   <CellInfo>  
      <!-- One or more cell property definitions -->  
   </CellInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Untergeordnete Elemente|Eine oder mehrere Definitionen der Zelleneigenschaften|  
  
## <a name="remarks"></a>Hinweise  
 Das **CellInfo** -Element enthält eine Auflistung der Zelleneigenschaften der Zellen, die in dem multidimensionalen Datensatz, der von einem **root** -Element mithilfe des **MDDataSet** -Datentyps zurückgegeben wird, enthalten sind. Jede Zelleneigenschaft in dem **CellInfo** -Element wird durch ein einzelnes XML-Element definiert, das jeweils ein **name** -Attribut und ein **type** -Attribut enthält. Das **name** -Attribut der Zelleneigenschaft entspricht dem Namen der OLE DB für die OLAP-Zelleneigenschaft, die durch das XML-Element dargestellt wird; das **type** -Attribut stellt den XML-Datentyp der Zelleneigenschaft dar. Der Name des XML-Elements wird verwendet, um den Wert der Zelleneigenschaft der Zellen zu identifizieren, die in dem **CellData** -Element des **root** -Elements enthalten sind.  
  
 Die folgende Syntax beschreibt die Definition einer Zelleneigenschaft:  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 Die benötigten Eigenschaften und ihre Werte können über eine Nutzung des Anforderungstyps DISCOVER_PROPERTIES mit der **Discover** -Methode abgerufen werden. Es gibt keine erforderliche Reihenfolge für die im **PropertyList** -Element aufgelisteten Eigenschaften.  
  
 Optional können Anbieter Standardwerte für einzelne Elemente oder Zelleneigenschaften im **AxisInfo** - oder **CellInfo** -Abschnitt angeben. Die Standardwerte können für eine kleinere Ergebnismenge sorgen, wenn die Eigenschaft immer oder fast immer den gleichen Wert hat. Zum Angeben eines Standardwerts für eine Eigenschaft kann das**Default** -Element optional als untergeordnetes Element von einem der Zelleneigenschaften-Definitionselemente angegeben werden. Das Fehlen eines Elements oder einer Zelleneigenschaft im Ergebnis deutet daher darauf hin, dass der angegebene Standardwert der Wert der Zelleneigenschaft ist.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt daher, wie die Zelleneigenschaften VALUE, FORMATTED_VALUE und FORMAT_STRING im **CellInfo** -Element dargestellt werden.  
  
```  
<OlapInfo>  
   ...  
      <CellInfo>  
         <Value name="VALUE"></Value>  
         <FmtValue name="FORMATTED_VALUE"></FmtValue>  
         <FormatString name="FORMAT_STRING"></FormatString>  
      </CellInfo>  
</OlapInfo>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

