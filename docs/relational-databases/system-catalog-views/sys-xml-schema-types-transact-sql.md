---
title: sys.xml_schema_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c7e95c7c4157ba4b4f5d8c162c7a095a35b8b2b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro XML-Schemakomponente zurück, die einem Typ entspricht. Dabei ist **symbol_space** gleich **T**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**||Erbt Spalten von [xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_abstract**|**bit**|1 = Typ ist ein abstrakter Typ. Alle Instanzen eines Elements dieses Typs müssen **xsi:type** verwenden, um auf einen abgeleiteten Typ hinzuweisen, der nicht abstrakt ist.<br /><br /> 0 = Typ ist nicht abstrakt. (Standard)|  
|**allows_mixed_content**|**bit**|1 = Gemischter Inhalt ist zulässig<br /><br /> 0 = Gemischter Inhalt ist nicht zulässig (Standard)|  
|**is_extension_blocked**|**bit**|1 = ersetzen durch eine Erweiterung des Typs in Instanzen blockiert ist, wenn das zugehörige Attribut in der **ComplexType** Definition oder der **BlockDefault** Attribut der übergeordneten \<Schema > elementinformationselement wird auf "Extension" oder "#all" festgelegt.<br /><br /> 0 = Ersetzen durch Erweiterung ist nicht blockiert.|  
|**is_restriction_blocked**|**bit**|1 = ersetzen durch eine Einschränkung des Typs in Instanzen blockiert ist, wenn das zugehörige Attribut in der **ComplexType** Definition oder der **BlockDefault** Attribut der übergeordneten \<Schema > elementinformationselement wird auf "Restriction" oder "#all" festgelegt.<br /><br /> 0 = Ersetzen durch Einschränkung ist nicht blockiert. (Standard)|  
|**is_final_extension**|**bit**|1 = der Ableitung durch Erweiterung des Typs ist nicht möglich, wenn das abschließende Attribut in der **ComplexType** Definition oder der **FinalDefault** Attribut der übergeordneten \<Schema > Elementinformationen Element wird auf "Extension" oder "#all" festgelegt.<br /><br /> 0 = Erweiterung ist zulässig. (Standard)|  
|**is_final_restriction**|**bit**|1 = das Ableiten anhand der Einschränkung des Typs ist nicht möglich, wenn das abschließende Attribut in das einfache oder **ComplexType** Definition oder die **FinalDefault** Attribut der übergeordneten \<Schema >-Element Informationselement wird auf "Restriction" oder "#all" festgelegt.<br /><br /> 0 = Einschränkung ist zulässig. (Standard)|  
|**is_final_list_member**|**bit**|1 = Dieser einfache Typ kann nicht als Elementtyp in einer Liste verwendet werden.<br /><br /> 0 = Dieser Typ ist ein komplexer Typ oder kann als Listenelementtyp verwendet werden. (Standard)|  
|**is_final_union_member**|**bit**|1 = Dieser einfache Typ kann nicht als Elementtyp eines Vereinigungstyps verwendet werden.<br /><br /> 0 = Dieser Typ ist ein komplexer Typ oder kann als Vereinigungselementtyp verwendet werden. (Standard)|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML-Schemas &#40; XML-Typsystem &#41; Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
