---
title: DISCOVER_PROPERTIES-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
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
ms.openlocfilehash: a5a68b41673466ef2e27846f598d070ee68903e7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Gibt eine Liste von Informationen und Werten zu den standardmäßigen und anwenderspezifischen Eigenschaften, die von unterstützt werden die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA)-Anbieter für die angegebene Datenquelle. Nicht unterstützte Eigenschaften werden nicht im zurückgegebenen Resultset aufgelistet.  
  
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
  
  
