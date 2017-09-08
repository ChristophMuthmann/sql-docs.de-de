---
title: Properties-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Properties Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Properties
- microsoft.xml.analysis.properties
- urn:schemas-microsoft-com:xml-analysis#Properties
- Properties
helpviewer_keywords:
- Properties element
ms.assetid: 0b5468e5-bf23-4d22-862f-72e27a9fff2f
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 77029875d3c2e84c1b48c4e1e5454f735f5a2752
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="properties-element-xmla"></a>Properties-Element (XMLA)
  Enthält XML für Analysis (XMAL)-Eigenschaften, die verwendet werden, indem Sie die [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) und [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methoden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Discover> <!-- or Execute -->  
...  
   <Properties>  
      <PropertyList>...</PropertyList>  
   </Properties>  
...  
</Discover>  
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
|Übergeordnete Elemente|[Ermitteln](../../../analysis-services/xmla/xml-elements-methods-discover.md), [ausführen](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|Untergeordnete Elemente|[PropertyList](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das **Properties** -Element repräsentiert XMLA-Eigenschaften, mit denen Aspekte der **Discover** -Methode und der **Execute** -Methode gesteuert werden. Dazu gehört das Definieren von Informationen, die für die Verbindung mit der Datenquelle erforderlich sind, das Angeben des Rückgabeformats des Resultsets oder das Angeben des Gebietsschemas, für das die Daten formatiert werden sollen.  
  
 Die benötigten Eigenschaften und ihre Werte können über eine Nutzung des Anforderungstyps DISCOVER_PROPERTIES mit der **Discover** -Methode abgerufen werden.  
  
## <a name="example"></a>Beispiel  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
