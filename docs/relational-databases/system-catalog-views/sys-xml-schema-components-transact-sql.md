---
title: Sys. xml_schema_components (Transact-SQL) | Microsoft Docs
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
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a3e5b71a36df056dbba198a86af316d32fb9eaf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro Komponente eines XML-Schemas zurück. Das Paar (**collection_id**, **namespace_id**) ist ein zusammengesetzter Fremdschlüssel für den Namespace, in dem es enthalten ist. Für benannte Komponenten sind die Werte für **symbol_space**, **name**, **scoping_xml_component_id**, **is_qualified**, **xml_namespace_id**und **xml_collection_id** eindeutig.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|Eindeutige ID der XML-Schemakomponente in der Datenbank.|  
|**xml_collection_id**|**int**|ID der XML-Schemaauflistung, die den Namespace dieser Komponente enthält.|  
|**xml_namespace_id**|**int**|ID des XML-Namespaces innerhalb der Auflistung.|  
|**is_qualified**|**bit**|1 = Diese Komponente besitzt einen expliziten Namespacequalifizierer.<br /><br /> 0 = Dies ist eine Komponente mit lokalem Bereich. In diesem Fall bezieht sich das Paar **namespace_id**, **collection_id**auf keinen Namespace in **targetNamespace**.<br /><br /> Bei Platzhalterkomponenten ist dieser Wert 1.|  
|**name**|**nvarchar**<br /><br /> **(4000)**|Eindeutiger Name der XML-Schemakomponente. Ist NULL, falls die Komponente keinen Namen trägt.|  
|**symbol_space**|**char(1)**|Bereich, in dem dieser Symbolname eindeutig ist, basierend auf **kind**:<br /><br /> N = Keiner<br /><br /> T = Typ<br /><br /> E = Element<br /><br /> M = Modell-Gruppe<br /><br /> A = Attribut<br /><br /> G = Attribut-Gruppe|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|Beschreibung des Bereichs, in dem dieser Symbolname eindeutig ist, basierend auf **kind**:<br /><br /> NONE<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**Art**|**char(1)**|Art der XML-Schemakomponente.<br /><br /> N = Beliebiger Typ (spezielle systeminterne Komponente)<br /><br /> Z = Beliebiger einfacher Typ (spezielle systeminterne Komponente)<br /><br /> P = Grundtyp (systeminterne Typen)<br /><br /> S = Einfacher Typ<br /><br /> L = Listentyp<br /><br /> U = Vereinigungstyp<br /><br /> C = Komplexer einfacher Typ (abgeleitet von Simple)<br /><br /> K = Komplexer Typ<br /><br /> E = Element<br /><br /> M = Modell-Gruppe<br /><br /> W = Element-Platzhalter<br /><br /> A = Attribut<br /><br /> G = Attribut-Gruppe<br /><br /> V = Attribut-Platzhalter|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|Beschreibung der Art der XML-Schemakomponente:<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**Ableitung**|**char(1)**|Ableitungsmethode für abgeleitete Typen:<br /><br /> N = Keine (nicht abgeleitet)<br /><br /> X = Erweiterung<br /><br /> R = Einschränkung<br /><br /> S = Ersetzung|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|Beschreibung der Ableitungsmethode für abgeleitete Typen:<br /><br /> NONE<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|ID der Komponente, aus der diese Komponente abgeleitet wird. Ist NULL, falls keine Komponente vorhanden ist.|  
|**scoping_xml_component_id**|**int**|Eindeutige ID der Komponente, die den Gültigkeitsbereich vorgibt. Ist NULL, falls keine Komponente vorhanden ist (globaler Gültigkeitsbereich).|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML-Schemas &#40; XML-Typsystem &#41; Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
