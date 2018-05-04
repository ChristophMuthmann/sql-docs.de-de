---
title: DISCOVER_LITERALS-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_LITERALS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dc239de2abb609aa035880c0cf9dd9217343c08c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt Informationen zu Literalen, einschließlich Datentypen und Werten, zurück, die vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis-Anbieter (XMLA) unterstützt werden.  
  
 Beim Aufrufen der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode mit der **DISCOVER_LITERALS** Enumerationswert in der [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) Element, das **Discover** Methode gibt die **DISCOVER_LITERALS** Rowset.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_LITERALS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LiteralName**|**DBTYPE_WSTR**||Der Name des in der Zeile beschriebenen Literals.<br /><br /> Beispiel: **DBLITERAL_LIKE_PERCENT**|  
|**LiteralValue**|**DBTYPE_WSTR**||Ein tatsächlicher Literalwert.<br /><br /> Z. B. wenn **LiteralName** ist **DBLITERAL_LIKE_PERCENT** und das Prozentzeichen (**%**) stimmt mit keinem oder mehreren Zeichen in einer LIKE-Klausel, die den Wert von der **LiteralValue** Spalte ist "**%**".|  
|**LiteralInvalidChars**|**DBTYPE_WSTR**||Die Zeichen, die im Literal nicht gültig sind.<br /><br /> Wenn Tabellennamen z. B. etwas anderes als ein numerisches Zeichen enthalten können, ist diese Zeichenfolge "**0123456789**".|  
|**LiteralInvalidStartingChars**|**DBTYPE_WSTR**||Die Zeichen, die nicht als erstes Zeichen des Literals verwendet werden dürfen. Wenn das Literal mit irgendeinem gültigen Zeichen beginnen kann, ist dies **null**.|  
|**LiteralMaxLength**|**DBTYPE_I4**||Es können maximal 250 Zeichen eingegeben werden. Wenn die Spalte über keine maximale Länge verfügt, ist der Wert -1 (Standardwert).|  
|**LiteralNameEnumValue**|**DBTYPE_I4**|||  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_LITERALS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**LiteralName**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS-Rowset & #40; XMLA & #41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
