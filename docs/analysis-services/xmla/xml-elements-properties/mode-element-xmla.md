---
title: Mode-Element (XMLA) | Microsoft Docs
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
- Mode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57c3450e8928b24dc03e2d5915983f39330d0b0c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mode-element-xmla"></a>Mode-Element (XMLA)
  Gibt den Modus an, durch das übergeordnete Element verwendet werden [Sperre](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) Element bei der Erstellung einer Sperre für ein angegebenes Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
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
|Übergeordnete Elemente|[Sperre](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [entsperren](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das übergeordnete **Lock** -Element verwendet das **Mode** -Element, um den Typ der auf einem Objekt zu erstellenden Sperre zu bestimmen. Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*CommitShared*|Auf dem angegebenen Objekt wird eine gemeinsame Sperre erstellt. Andere gemeinsame Sperren können für das gleiche Objekt erstellt werden.<br /><br /> Eine gemeinsame Sperre verhindert, dass Transaktionen, die mit der Schreibvorgänge, z. B. ein [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methodenaufruf ausgeführt ein [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) Befehl auf einem angegebenen Objekt, bis die gemeinsame Sperre aufgehoben wird. Eine gemeinsame Sperre verhindert nicht, dass Transaktionen, die Lesevorgänge an, wie z. B. enthalten eine [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methodenaufruf oder ein **Execute** Methodenaufruf ausgeführt eine [Anweisung](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) -Befehl aus Ausführen eines Commits für.|  
|*CommitExclusive*|Auf dem angegebenen Objekt wird eine exklusive Sperre erstellt. Andere gemeinsame oder exklusive Sperren können nicht für das gleiche Objekt erstellt werden.<br /><br /> Eine exklusive Sperre verhindert die Commitausführung von Transaktionen, die entweder Lese- oder Schreibvorgänge auf einem angegebenen Objekt enthalten, bis die exklusive Sperre aufgehoben ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [ID-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Object-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

