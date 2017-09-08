---
title: Row-Element (XMLA) | Microsoft Docs
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
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52bc6d400340375163fd9ae8b285c071249a88f7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="row-element-xmla"></a>row-Element (XMLA)
  Enthält eine einzelne Zeile mit Daten für eine [Stamm](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) Element, das tabellarische Daten zurückgegebenes enthält eine [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methodenaufruf.  
  
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
|Übergeordnete Elemente|[Stamm](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) (mithilfe der [Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) -Datentyp)|  
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
  
 Weitere Informationen über spaltenbenennung und Schemainformationen für tabellarische Daten finden Sie unter [Rowset-Datentyp &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
