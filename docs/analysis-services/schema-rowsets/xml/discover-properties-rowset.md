---
title: DISCOVER_PROPERTIES-Rowset | Microsoft Docs
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
apiname: DISCOVER_PROPERTIES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b695d3affd1783782e1eb8bde27d6c90157e4bab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES-Rowset
  Gibt eine Liste mit Informationen und Werten zu den standardmäßigen und anwenderspezifischen Eigenschaften zurück, die vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA-Anbieter (XML for Analysis) für die angegebene Datenquelle unterstützt werden. Nicht unterstützte Eigenschaften werden nicht im zurückgegebenen Resultset aufgelistet.  
  
 Beim Aufrufen der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode mit der **DISCOVER_PROPERTIES** Enumerationswert in der [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) Element, das **Discover** Methode gibt die **DISCOVER_PROPERTIES** Rowset...  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_PROPERTIES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typ|Länge|Description|  
|-----------------|----------|------------|-----------------|  
|**Eigenschaftenname**|**DBTYPE_WSTR**||Der Name der Eigenschaft.|  
|**PropertyDescription**|**DBTYPE_WSTR**||Eine lokalisierbare Textbeschreibung der Eigenschaft. Kann **NULL**zurückgeben.|  
|**PropertyType**|**DBTYPE_WSTR**||Der XML-Datentyp der Eigenschaft.<br /><br /> Kann **NULL**zurückgeben.|  
|**PropertyAccessType**|**DBTYPE_WSTR**||Der Zugriff für die Eigenschaft. Der Wert kann **Read**, **Write**oder **ReadWrite**lauten.|  
|**"IsRequired"**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob eine Eigenschaft erforderlich ist.<br /><br /> True, wenn eine Eigenschaft erforderlich ist; False, wenn keine erforderlich ist.<br /><br /> Kann **NULL**zurückgeben.|  
|**Wert**|**DBTYPE_WSTR**||Der aktuelle Wert der Eigenschaft.<br /><br /> Kann **NULL**zurückgeben.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_PROPERTIES** -Rowset kann auf die in der folgenden Tabelle aufgeführte Spalte eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**Eigenschaftenname**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis – Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
