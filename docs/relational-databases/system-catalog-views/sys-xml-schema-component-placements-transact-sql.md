---
title: Sys. xml_schema_component_placements (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7303664cea2b29938f666f2dd74f86749fa443e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysxmlschemacomponentplacements-transact-sql"></a>sys.xml_schema_component_placements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro Platzierung für XML-Schemakomponenten zurück.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID der XML-Schemakomponente, die diese Platzierung besitzt.|  
|**placement_id**|**int**|ID der Platzierung. Diese ist eindeutig innerhalb der besitzenden XML-Schemakomponente.|  
|**placed_xml_component_id**|**int**|ID der platzierten XML-Schemakomponente.|  
|**is_default_fixed**|**bit**|1 = Der Standardwert ist ein fester Wert. Dieser Wert kann in einer XML-Instanz nicht überschrieben werden.<br /><br /> 0 = Der Wert kann überschrieben werden. (Standard)|  
|**min_occurrences**|**int**|Mindestzahl der platzierten Komponenten.|  
|**max_occurrences**|**int**|Höchstzahl der platzierten Komponenten.|  
|**default_value**|**Nvarchar (4000)**|Standardwert, sofern bereitgestellt. Ist NULL, wenn kein Standardwert angegeben wird.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML-Schemas &#40;XML-Typsystem&#41; Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
