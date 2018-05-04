---
title: Row-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- row Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords:
- row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d2e8b859f6e05497666edcf0e763628ebd037b43
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="row-element-xmla"></a>row-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält eine einzelne Datenzeile für ein [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) -Element, das tabellarische Daten enthält, die von einem [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) - oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methodenaufruf zurückgegeben wurden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
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
|Übergeordnete Elemente|[root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) (mit [Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) -Datentyp)|  
|Untergeordnete Elemente|Ein oder mehrere Column-Elemente.|  
  
## <a name="remarks"></a>Hinweise  
 Jede von einem **root** -Element ausgegebene Zeile, die tabellarische Daten enthält, verfügt über eine entsprechendes **row** -Element. Jede Spalte im **root** -Element wird durch ein separates XML-Element dargestellt. Beim Wert der Spalte des **row** -Elements handelt es sich um die Daten, die im XML-Element enthalten sind. Der Name der Spalte entspricht dem Namen des XML-Elements.  
  
 Der NULL-Wert für eine Spalte innerhalb einer Zeile kann auf zwei Arten ausgedrückt werden:  
  
-   Ein fehlendes Column-Element deutet darauf hin, dass die Spalte NULL ist.  
  
-   Das Column-Element kann das `xsi:nil='true'` -Attribut nutzen, um auf den NULL-Wert hinzuweisen.  
  
 Beispiel: enthält eine Zeile eine einzelne Spalte mit Namen Store_Name und ist der Wert NULL, kann dies so ausgedrückt werden:  
  
```  
<row>  
</row>  
```  
  
 Oder:  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
 Wenn ein Column-Element einen Fehler enthält, stellt ein **Error** -Element, wie im folgenden Beispiel beschrieben, Informationen über einen Fehler bereit:  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 Weitere Informationen über spaltenbenennung und Schemainformationen für tabellarische Daten finden Sie unter [Rowset-Datentyp & #40; XMLA & #41; ](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
