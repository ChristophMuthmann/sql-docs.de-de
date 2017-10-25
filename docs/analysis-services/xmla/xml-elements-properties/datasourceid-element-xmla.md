---
title: DataSourceID-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DataSourceID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.datasourceid
- urn:schemas-microsoft-com:xml-analysis#DataSourceID
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 695522c7-acca-420a-a5fb-f01f3fd9a96b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eb3374f4a2bc9da44263ed65a4247903671e03dd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datasourceid-element-xmla"></a>DataSourceID-Element (XMLA)
  Identifiziert die Datenquelle verwendet werden, indem eine [Speicherort](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) -Element während einer [Sicherung](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), oder [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) Befehl.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Location>  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Speicherort](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **DataSourceID** -Element enthält den Namen der Datenquelle auf der Quellinstanz, der die Remoteinstanz identifiziert, auf der Remotepartitionsinformationen gesichert, wiederhergestellt oder synchronisiert werden.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Remotepartitionen finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ConnectionString-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)   
 [DataSourceType-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

