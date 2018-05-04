---
title: EnumString-Datentyp (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- EnumString Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords:
- EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 11f789c735a80ece07c1c59d18232dfa80a848da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="enumstring-data-type-xmla"></a>EnumString-Datentyp (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Definiert einen abgeleiteten Datentyp, der für einen gegebenen Enumerator einen Satz genannter Konstanten darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|**Zeichenfolge**|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|Keine|  
|Abgeleitete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 XML for Analysis (XMLA) schränkt Zeichenfolgenwerte mithilfe von Enumerationen auf einen Satz überprüfbarer Einstellungen ein. **EnumString** verwendet den standardmäßig **string** -XML-Datentyp. Die bestimmten Werte für jede der genannten Konstanten werden mit der Enumeratordefinition angegeben. Enumeratoren werden definiert, indem Sie sie zum Hinzufügen der [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) -Schemarowset, und kann abgerufen werden, indem die [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode mit dem DISCOVER_ENUMERATORS-Anforderungstyp.  
  
 Die folgende Tabelle beschreibt die Enumeratoren, die von einer Instanz von unterstützt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Enumerator|Description|  
|----------------|-----------------|  
|ProviderType|Unterstützt die ProviderType-Spalte in der [DISCOVER_DATASOURCES](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md) -Schemarowset, die den Typ der Daten bestimmt, die von zurückgegeben werden, kann ein [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.<br /><br /> Diese Enumeration unterstützt zusätzlich die XMLA-Eigenschaft **ProviderType**, der den von unterstützten Providertyp bestimmt eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz. Diese Enumeration wird auch im DISCOVER_DATASOURCES-Schemarowset verwendet.<br /><br /> Weitere Informationen zu **ProviderType**, finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|AuthenticationMode|Unterstützt die AuthenticationMode-Spalte im DISCOVER_DATASOURCES-Schemarowset, die die Sicherheitsanmeldeinformationen bestimmt, die übergeben werden, müssen für den Zugriff auf eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.|  
|PropertyAccessType|Unterstützt die PropertyAccessType-Spalte in der [DISCOVER_PROPERTIES](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md) -Schemarowset, die für ein XMLA-Eigenschaft verfügbaren Zugriffstyp bestimmt.|  
|StateSupport|Unterstützt die XMLA-Eigenschaft, **Statusunterstützungswerte**, bestimmt die Ebene der statusbehaftung, die durch eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.<br /><br /> Weitere Informationen zu **Statusunterstützungswerte**, finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|StateActionVerb|Enthält eine Liste der Verben, die von XMLA in SOAP-Headern unterstützt und zum Starten, Identifizieren und Beenden einer Sitzung verwendet werden.<br /><br /> Weitere Informationen zu Sitzungen finden Sie unter [Verwalten von Verbindungen und Sitzungen &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).|  
|ResultsetFormat|Unterstützt die XMLA-Eigenschaft, **Format**, der den Typ des in der zurückgegebenen Daten bestimmt eine [Root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) Element.<br /><br /> Weitere Informationen zu **Format**, finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetAxisFormat|Unterstützt die XMLA-Eigenschaft, **AxisFormat**, die das Format der Achseninformationen bestimmt, die von einem **root** -Element zurückgegeben werden, das multidimensionale Daten enthält.<br /><br /> Weitere Informationen zu **AxisFormat**, finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetContents|Unterstützt die XMLA-Eigenschaft, **Content**, die bestimmt, ob Metadaten oder Daten in einem **root** -Element zurückgegeben werden.<br /><br /> Weitere Informationen zu **Content**, finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|MDXSupportLevel|Unterstützt die XMLA-Eigenschaft, **MDXSupport**, womit MDX (Multidimensional Expressions) unterstützt, die auf eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.<br /><br /> Weitere Informationen zu **MDXSupport**, finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Datentypen &#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
