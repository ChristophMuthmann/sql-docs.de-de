---
title: DISCOVER_KEYWORDS-Rowset (XMLA) | Microsoft Docs
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
- DISCOVER_KEYWORDS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0a8933c872bcc0947e8bff34cf3fbbc57394b9cf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS-Rowset (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt Informationen über vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis-Anbieter (XMLA) reservierte Schlüsselwörter zurück.  
  
 Wenn Sie die [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) -Methode mit dem **DISCOVER_KEYWORDS** -Enumerationswert im [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) -Element aufrufen, gibt die **Discover** -Methode das **DISCOVER_KEYWORDS** -Rowset zurück.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_KEYWORDS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Schlüsselwort**|**DBTYPE_WSTR**||Eine Liste aller von einem Anbieter reservierten Schlüsselwörter.<br /><br /> Beispiel: **AND**|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_KEYWORDS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**Schlüsselwort**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_LITERALS-Rowset](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)  
  
  
