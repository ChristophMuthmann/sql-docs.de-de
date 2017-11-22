---
title: Sys. xml_schema_facets (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df9761b05605282e125c9fee091cde0dfa345012
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysxmlschemafacets-transact-sql"></a>sys.xml_schema_facets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro Facet (Einschränkung) einer Definition vom Typ XML zurück (entspricht **sys.xml_types**).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID der XML-Komponente (Typ), zu der dieses Facet gehört.|  
|**facet_id**|**int**|ID (1-basierte Ordnungszahl) des Facets, die innerhalb der Komponenten-ID eindeutig ist.|  
|**Art**|**char(2)**|Art des Facets:<br /><br /> LG = Länge<br /><br /> LN = Mindestlänge<br /><br /> LX = Höchstlänge<br /><br /> PT = Muster (regulärer Ausdruck)<br /><br /> EU = Enumeration<br /><br /> IN = Minimaler eingeschlossener Wert<br /><br /> IX = Maximaler eingeschlossener Wert<br /><br /> EN = Minimaler ausgeschlossener Wert<br /><br /> EX = Maximaler ausgeschlossener Wert<br /><br /> DT = Ziffern gesamt<br /><br /> DF = Verhältnis Ziffern<br /><br /> WS = Leerstellennormalisierung|  
|**kind_desc**|**Nvarchar (60)**|Beschreibung der Art des Facets:<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> PATTERN<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = Facet weist einen festen, vordefinierten Wert auf.<br /><br /> 0 = Kein fester Wert. (Standard)|  
|**Wert**|**Nvarchar (4000)**|Fester, vordefinierter Wert des Facets.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML-Schemas &#40; XML-Typsystem &#41; Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
