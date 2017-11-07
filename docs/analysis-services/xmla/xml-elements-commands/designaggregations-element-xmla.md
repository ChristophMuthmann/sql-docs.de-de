---
title: DesignAggregations-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DesignAggregations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DesignAggregations
- microsoft.xml.analysis.designaggregations
- http://schemas.microsoft.com/analysisservices/2003/engine#DesignAggregations
helpviewer_keywords:
- DesignAggregations command
ms.assetid: 4c419dbc-7405-40aa-8ddd-6b46685a297d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a20166ec005068195d93ee22c40837213944445
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="designaggregations-element-xmla"></a>DesignAggregations-Element (XMLA)
  Erstellt Aggregationen für einen Aggregationsentwurf auf einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[Materialisieren](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md), [Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [Optimierung](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md), [Abfragen](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md), [Schritte](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md), [Speicher](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md), [Zeit](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Der **DesignAggregations** -Befehl wird verwendet, um Aggregationsdefinitionen zu generieren, die von einem Aggregationsentwurf gespeichert werden. Ein Aggregationsentwurf kann dann verwendet werden, um Aggregationen für eine Partition zu materialisieren, und kann zwischen Partitionen neu verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

