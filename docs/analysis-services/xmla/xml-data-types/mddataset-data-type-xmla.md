---
title: MDDataSet-Datentyp (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDDataSet Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ed0c285f34f55f89b571cf671cf6601e5a81490
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mddataset-data-type-xmla"></a>MDDataSet-Datentyp (XMLA)
  Definiert einen abgeleiteten Datentyp, der vom zurückgegebenen mehrdimensionale Daten darstellt, der die [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis:mddataset  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <OlapInfo>...</OlapInfo>  
   <Axes>...</Axes>  
   <CellData>...</CellData>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[Resultset](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Achsen](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md), [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md), [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Abgeleitete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der **MDDataSet** -Datentyp stellt das OLAP-orientierte Rowset (oder Dataset) bereit, das erforderlich ist, um OLAP-Daten in XML darzustellen. Die Inhalte dieses Rowsets können je nach den Werten der variieren die **Content** und **Format** Eigenschaften in der [Eigenschaften](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) Auflistung von der  **Führen Sie** Methode. Weitere Informationen zu den **Content** und **Format** Eigenschaften finden Sie in [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Grundlegende Informationen zu OLE DB für OLAP-Datensatzstrukturen finden Sie unter "MDDataSet-Datentypzuordnung zu OLE DB" in der XML 1.1-Spezifikation (XML for Analysis). Ein vollständiges XSD-Beispiel (XML Schema Definition Language) für den **MDDataSet** -Datentyp finden Sie unter "Appendix D: MDDataSet Example" in der XML 1.1-Spezifikation (XML for Analysis).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Datentypen &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  

