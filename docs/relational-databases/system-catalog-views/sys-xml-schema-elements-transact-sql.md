---
title: Sys. xml_schema_elements (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32c5a61fe630192b6ff62a41804db22524f481a5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysxmlschemaelements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro XML-Schemakomponente, die ein Typ ist **Symbol_space** von **E**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**|**--**|Erbt Spalten von [xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_default_fixed**|**bit**|1 = Standardwert ist ein fester Wert. Dieser Wert kann nicht in XML-Instanz überschrieben werden.<br /><br /> 0 = Standardwert ist kein fester Wert für das Element. (Standard).|  
|**is_abstract**|**bit**|1 = Element ist abstrakt und kann in einem Instanzdokument nicht verwendet werden. Ein Mitglied der Ersetzungsgruppe des Elements muss im Instanzdokument vorkommen.<br /><br /> 0 = Element ist nicht abstrakt. (Standard).|  
|**is_nillable**|**bit**|1 = Element kann ein NULL-Wert sein.<br /><br /> 0 = Element kann kein NULL-Wert sein. (Standard)|  
|**must_be_qualified**|**bit**|1 = Element muss explizit als Namespace qualifiziert werden.<br /><br /> 0 = Element kann implizit als Namespace qualifiziert werden. (Standard)|  
|**is_extension_blocked**|**bit**|1 = Ersetzen durch eine Instanz eines Erweiterungstyps ist blockiert.<br /><br /> 0 = Ersetzen durch Erweiterungstyp ist zulässig. (Standard)|  
|**is_restriction_blocked**|**bit**|1 = Ersetzen durch eine Instanz eines Einschränkungstyps ist blockiert.<br /><br /> 0 = Ersetzen durch Einschränkungstyp ist zulässig. (Standard)|  
|**is_substitution_blocked**|**bit**|1 = Instanz einer Ersetzungsgruppe kann nicht verwendet werden.<br /><br /> 0 = Ersetzen durch Ersetzungsgruppe ist zulässig. (Standard)|  
|**is_final_extension**|**bit**|1 = Ersetzen durch eine Instanz eines Erweiterungstyps ist nicht zulässig.<br /><br /> 0 = Ersetzen in einer Instanz eines Erweiterungstyps ist zulässig. (Standard)|  
|**is_final_restriction**|**bit**|1 = Ersetzen durch eine Instanz eines Einschränkungstyps ist nicht zulässig.<br /><br /> 0 = Ersetzen in einer Instanz eines Einschränkungstyps ist zulässig. (Standard)|  
|**Standardwert**|**Nvarchar (4000)**|Standardwert des Elements. NULL, wenn kein Standardwert bereitgestellt wird.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML-Schemas &#40; XML-Typsystem &#41; Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
