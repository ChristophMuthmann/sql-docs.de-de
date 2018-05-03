---
title: Abfrage-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Query Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords:
- Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb9a015347bf0edccedecd59fe1d66785a1c613f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="query-element-xmla"></a>Query-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält eine Abfrage innerhalb der [Abfragen](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md) Auflistung für die [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) -Befehl während verwendungsbasierter Optimierung.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
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
|Übergeordnete Elemente|[Abfragen](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der **DesignAggregations** -Befehl unterstützt verwendungsbasierte Optimierung durch die Einbindung ein oder mehrerer **Query** -Elemente in die **Queries** -Auflistung des Befehls. Jedes **Query** -Element stellt eine Zielabfrage dar, die der Entwurfsprozess nutzt, um Aggregationen zu definieren, die auf die am häufigsten verwendeten Abfragen abzielen. Sie können entweder Ihre eigenen Zielabfragen festlegen oder die Informationen nutzen, die von einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] im Abfrageprotokoll gespeichert werden, um Informationen über die am häufigsten verwendeten Abfragen abzurufen.  
  
 Wenn Sie Aggregationen iterativ entwerfen, nur müssen Sie zielabfragen im ersten übergeben **DesignAggregations** Befehl, weil die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz diese zielabfragen speichert und verwendet diese Abfragen während der nachfolgenden  **DesignAggregations** Befehle. Nachdem Sie Zielabfragen im ersten **DesignAggregations** -Befehl eines iterativen Prozesses weitergegeben haben, generiert jeder darauf folgende **DesignAggregations** -Befehl, der über Zielabfragen in der **Queries** -Eigenschaft verfügt, einen Fehler.  
  
 Das **Query** -Element enthält einen durch Trennzeichen getrennten Wert, der die folgenden Argumente beinhaltet:  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *Häufigkeit*  
 Ein Gewichtungsfaktor, der der Anzahl der Male entspricht, die eine Abfrage zuvor ausgeführt wurde. Wenn das **Query** -Element eine neue Abfrage darstellt, gibt der *Frequency* -Wert den Gewichtungsfaktor an, der vom Entwurfsprozess für die Evaluierung der Abfrage verwendet wird. Bei steigendem Häufigkeitswert, steigt die Gewichtung auf die Abfrage während des Entwurfsprozesses.  
  
 *DataSet*  
 Eine numerische Zeichenfolge, die festlegt, welche Attribute einer Dimension in die Abfrage eingebunden werden. Diese Zeichenfolge muss die gleiche Anzahl an Zeichen wie die Anzahl an Attributen in der Dimension haben. null (0) zeigt an, dass das Attribut an der angegebenen Ordnungsposition für die angegebene Dimension nicht in der Abfrage enthalten ist. Eins (1) zeigt an, dass das Attribut an der angegebenen Ordnungsposition für die angegebene Dimension in der Abfrage enthalten ist.  
  
 Beispielsweise bezieht sich die Zeichenfolge "011" auf eine Abfrage mit einer Dimension mit drei Attributen, von denen das zweite und dritte Attribut in der Abfrage enthalten sind.  
  
> [!NOTE]  
>  Einige Attribute sind von der Berücksichtigung im Dataset ausgenommen. Weitere Informationen über ausgenommene Attribute finden Sie unter [Properties (XMLA)](../../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md).  
  
 Jede Dimension in der Measuregruppe, die einen Aggregationsentwurf enthält, wird durch einen *Dataset* -Wert im **Query** -Element dargestellt. Die Reihenfolge der *Dataset* -Werte muss der Reihenfolge der Dimensionen entsprechen, die in die Measuregruppe eingebunden sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwerfen von Aggregationen & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
