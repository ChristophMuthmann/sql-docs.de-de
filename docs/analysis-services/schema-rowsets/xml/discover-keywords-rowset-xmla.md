---
title: DISCOVER_KEYWORDS-Rowset (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 232bbcfb4d5cf1dfc181a0c6d8879e4390f61a9e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS-Rowset (XMLA)
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
  
  

