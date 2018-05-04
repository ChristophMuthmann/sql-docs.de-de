---
title: ConnectionString-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ConnectionString Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 58bde607d580f8b9dcabdd861144f58d76bef53f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connectionstring-element-xmla"></a>ConnectionString-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält eine Verbindungszeichenfolge, die vom übergeordneten [Location](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) -Element oder [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) -Element verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|Siehe Tabelle unten.|  
  
|Vorgänger oder übergeordnetes Element|Kardinalität|  
|------------------------|-----------------|  
|[Speicherort](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|1-1: Erforderliches Element, das nur einmal auftritt.|  
|[Quelle](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Location](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Für **Location** -Elemente enthält das **ConnectionString** -Element die Verbindungszeichenfolge, die vom **Restore** - oder **Synchronize** -Befehl entweder zum Aktualisieren einer lokalen Datenquelle oder zum Verbinden mit einer Remoteinstanz verwendet wird.  
  
 Für **Source** -Elemente enthält das **ConnectionString** -Element die Verbindungszeichenfolge, die vom **Synchronize** -Befehl zum Verbinden mit der Quellinstanz verwendet wird.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Objekten finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Restore-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Synchronisieren Sie-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
