---
title: MDSCHEMA_LEVELS-Rowset | Microsoft Docs
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
- MDSCHEMA_LEVELS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7eb78b431b77dadfe216db5e30e77e9d5722b2a8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemalevels-rowset"></a>MDSCHEMA_LEVELS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Beschreibt jede Ebene innerhalb einer bestimmten Hierarchie an.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **MDSCHEMA_LEVELS** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Der Name des Katalogs, zu dem diese Ebene gehört. **NULL** , wenn der Anbieter keine Kataloge unterstützt.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Der Name des Schemas, zu dem diese Ebene gehört. **NULL** , wenn der Anbieter keine Schemas unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Der Name des Cubes, zu dem diese Ebene gehört.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Der eindeutige Name der Dimension, zu der diese Ebene gehört. Für Anbieter, die eindeutige Namen durch eine Einschränkung generieren, ist jede Komponente dieses Namens begrenzt.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Der eindeutige Name der Hierarchie. Wenn die Ebene zu mehreren Hierarchien gehört, gibt es eine Zeile für jede Hierarchie, zu der die Ebene gehört. Für Anbieter, die eindeutige Namen durch eine Einschränkung generieren, ist jede Komponente dieses Namens begrenzt.|  
|**EBENENNAME**|**DBTYPE_WSTR**|Der Name der Ebene.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Der ordnungsgemäß mit Escapezeichen versehene eindeutige Name der Ebene.|  
|**LEVEL_GUID**|**DBTYPE_GUID**|Nicht unterstützt.|  
|**LEVEL_CAPTION**|**DBTYPE_WSTR**|Eine Bezeichnung oder Beschriftung, die der Hierarchie zugeordnet ist. Wird hauptsächlich für Anzeigezwecke verwendet. Wenn keine Beschriftung vorhanden, **Ebenenname** zurückgegeben wird.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|Der Abstand der Ebene vom Stamm der Hierarchie. Stammebene entspricht null (**0)**.|  
|**LEVEL_CARDINALITY**|**DBTYPE_UI4**|Die Anzahl der Elemente in der Ebene.|  
|**LEVEL_TYPE**|**DBTYPE_I4**|Der Typ der Ebene:<br /><br /> **MDLEVEL_TYPE_GEO_CONTINENT** (**0x2001**)<br /><br /> **MDLEVEL_TYPE_GEO_REGION** (**0 x 2002**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTRY** (**0x2003**)<br /><br /> **MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE** (**0x2004**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTY** (**0x2005**)<br /><br /> **MDLEVEL_TYPE_GEO_CITY** (**0x2006**)<br /><br /> **MDLEVEL_TYPE_GEO_POSTALCODE** (**0x2007**)<br /><br /> **MDLEVEL_TYPE_GEO_POINT** (**0x2008**)<br /><br /> **MDLEVEL_TYPE_ORG_UNIT** (**0x1011**)<br /><br /> **MDLEVEL_TYPE_BOM_RESOURCE** (**0x1012**)<br /><br /> **MDLEVEL_TYPE_QUANTITATIVE** (**0x1013**)<br /><br /> **MDLEVEL_TYPE_ACCOUNT** (**0x1014**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER** (**0x1021**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_GROUP** (**0x1022**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD** (**0x1023**)<br /><br /> **MDLEVEL_TYPE_PRODUCT** (**0x1031**)<br /><br /> **MDLEVEL_TYPE_PRODUCT_GROUP** (**0x1032**)<br /><br /> **MDLEVEL_TYPE_SCENARIO** (**0x1015**)<br /><br /> **MDLEVEL_TYPE_UTILITY** (**0x1016**)<br /><br /> **MDLEVEL_TYPE_PERSON** (**0x1041**)<br /><br /> **MDLEVEL_TYPE_COMPANY** (**0x1042**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_SOURCE** (**0x1051**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_DESTINATION** (**0x1052**)<br /><br /> **MDLEVEL_TYPE_CHANNEL** (**0x1061**)<br /><br /> **MDLEVEL_TYPE_REPRESENTATIVE** (**0x1062**)<br /><br /> **MDLEVEL_TYPE_PROMOTION** (**0x1071**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine lesbare Beschreibung der Ebene. NULL, wenn keine Beschreibung vorhanden ist.|  
|**CUSTOM_ROLLUP_SETTINGS**|**DBTYPE_I4**|Eine Bitmap, die die benutzerdefinierten Rollupoptionen angibt:<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_EXPRESSION** (**0 x 01**) gibt an, ein Ausdruck für diese Ebene vorhanden ist. (Veraltet)<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_COLUMN** (**0 x 02**) gibt an, dass eine benutzerdefinierte Rollupspalte für diese Ebene vorhanden ist.<br /><br /> **MDLEVELS_SKIPPED_LEVELS** (**0 x 04**) gibt an, dass eine übersprungene Ebene, die Elementen dieser Ebene zugeordnet.<br /><br /> **MDLEVELS_CUSTOM_MEMBER_PROPERTIES** (**0 x 08**) gibt an, dass die Elemente der Ebene über benutzerdefinierte Elementeigenschaften verfügen.<br /><br /> **MDLEVELS_UNARY_OPERATOR** (**0 x 10**) gibt an, dass Elemente auf der Ebene über unäre Operatoren verfügen.|  
|**LEVEL_UNIQUE_SETTINGS**|**DBTYPE_I4**|Eine Bitmap, die angibt, welche Spalten eindeutige Werte enthalten, wenn die Ebene nur Elemente mit eindeutigen Namen oder Schlüsseln enthält. Die Datei Msmd.h definiert die folgenden Bitwertkonstanten für diese Bitmap:<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)<br /><br /> **MDDIMENSIONS_MEMBER_NAME_UNIQUE** (**2**)<br /><br /> <br /><br /> Beachten Sie, dass der Schlüssel immer in eindeutig [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Der Name wird eindeutig sein, wenn die Einstellung für das Attribut **UniqueInDimension** oder **UniqueInAttribute**|  
|**LEVEL_IS_VISIBLE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Ebene sichtbar ist.<br /><br /> Es wird immer True zurückgegeben. Wenn die Ebene nicht sichtbar ist, wird sie nicht im Schemarowset angezeigt.|  
|**LEVEL_ORDERING_PROPERTY**|**DBTYPE_WSTR**|Die ID des Attributs, anhand dessen die Ebene sortiert wird.|  
|**LEVEL_DBTYPE**|**DBTYPE_I4**|Die **DBTYPE** -Enumeration der Elementschlüsselspalte, die für das Ebenenattribut verwendet wird.<br /><br /> NULL, wenn verkettete Schlüssel als Elementschlüsselspalte verwendet werden.|  
|**LEVEL_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|Gibt immer NULL zurück.|  
|**LEVEL_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|Die SQL-Darstellung der Ebenenelementnamen.|  
|**LEVEL_KEY_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|Die SQL-Darstellung der Ebenenelement-Schlüsselwerte.|  
|**LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|Die SQL-Darstellung der eindeutigen Ebenennamen.|  
|**LEVEL_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**|Der Name der Attributhierarchie, die die Quelle der Ebene bereitstellt.|  
|**LEVEL_KEY_CARDINALITY**|**DBTYPE_UI2**|Die Anzahl der Spalten im Ebenenschlüssel.|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|Eine Bitmap, die definiert, wie die Quelle der Ebene bestimmt wird:<br /><br /> **MD_ORIGIN_USER_DEFINED** gibt Ebenen in einer benutzerdefinierten Hierarchie.<br /><br /> **MD_ORIGIN_ATTRIBUTE** gibt Ebenen in einer Attributhierarchie.<br /><br /> **MD_ORIGIN_KEY_ATTRIBUTE** gibt Ebenen in einer schlüsselattributhierarchie.<br /><br /> **MD_ORIGIN_INTERNAL** gibt Ebenen in Attributhierarchien, die nicht aktiviert sind.|  
  
 Das Rowset wird sortiert nach **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ UNIQUE_NAME**, **LEVEL_NUMBER**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **MDSCHEMA_LEVELS** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**EBENENNAME**|**DBTYPE_WSTR**|Optional.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|(Optional) Eine standardeinschränkung ist faktisch auf **MD_USER_DEFINED** und **md_system_enabled gültig**|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**LEVEL_VISIBILITY**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden Werte:<br /><br /> 1 Sichtbar<br /><br /> 2 Nicht sichtbar|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
