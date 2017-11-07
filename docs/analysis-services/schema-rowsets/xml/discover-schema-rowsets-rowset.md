---
title: DISCOVER_SCHEMA_ROWSETS-Rowsets | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_SCHEMA_ROWSETS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ba7d3abc8f5ba5fdb941a8f97901d35c20f6b42
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discoverschemarowsets-rowset"></a>DISCOVER_SCHEMA_ROWSETS-Rowsets
  Gibt die Namen, Einschränkungen, Beschreibungen und anderen Informationen für alle Enumerationswerte und zusätzlichen anbieterspezifischen Enumerationswerte zurück, die vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis-Anbieter (XMLA) unterstützt werden.  
  
 Beim Aufrufen der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode mit der **DISCOVER_SCHEMA_ROWSETS** Enumerationswert in der [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) Element, das **Discover**Methode gibt die **DISCOVER_SCHEMA_ROWSETS** Rowset.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das DISCOVER_SCHEMA_ROWSETS-Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SchemaName**|**DBTYPE_WSTR**||Der Name des Schemas oder der Anforderung. Diese Anforderung gibt die Werte der *RequestTypes* -Enumeration zurück.|  
|**SchemaGuid**|**DBTYPE_GUID**||Die GUID des Schemas.|  
|**Einschränkungen**|**DBTYPE_HCHAPTER**||Ein Array von vom Anbieter unterstützten Einschränkungen.|  
|**Description**|**DBTYPE_WSTR**||Eine lokalisierbare Beschreibung des Schemas.|  
|**RestrictionsMask**|**DBTYPE_UI8**|||  
  
 Dieses Schemarowset ist nicht sortiert.  
  
 Für einen Anbieter, der drei Einschränkungen für das DBSCHEMA_MEMBERS-Schemarowset unterstützt, kann das **Restrictions** -Array das folgende Ergebnis zurückgeben. Die Elemente im Ergebnis verweisen auf Spaltennamen im Schema.  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_SCHEMA_ROWSETS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**SchemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

