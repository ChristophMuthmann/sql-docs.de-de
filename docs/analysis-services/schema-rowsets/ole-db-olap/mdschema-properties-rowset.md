---
title: MDSCHEMA_PROPERTIES-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- MDSCHEMA_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7243eae7198e9ae22df7fc661f005b51eb8db02e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemaproperties-rowset"></a>MDSCHEMA_PROPERTIES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Beschreibt die Eigenschaften von Elementen innerhalb einer Datenbank.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **MDSCHEMA_PROPERTIES** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||Der Name der Datenbank.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Der Name des Schemas, zu dem diese Eigenschaft gehört. **NULL** , wenn der Anbieter keine Schemas unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Der Name des Cubes.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||Der eindeutige Name der Dimension. Für Anbieter, die eindeutige Namen durch eine Einschränkung generieren, ist jede Komponente dieses Namens begrenzt.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||Der eindeutige Name der Hierarchie. Für Anbieter, die eindeutige Namen durch eine Einschränkung generieren, ist jede Komponente dieses Namens begrenzt.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||Der eindeutige Name der Ebene, zu der diese Eigenschaft gehört. Wenn der Anbieter keine benannte Ebenen unterstützt, sollte es zurückgeben der **DIMENSION_UNIQUE_NAME** Wert für dieses Feld. Für Anbieter, die eindeutige Namen durch eine Einschränkung generieren, ist jede Komponente dieses Namens begrenzt.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||Der eindeutige Name des Elements, zu dem diese Eigenschaft gehört. Wird für Datenspeicher verwendet, die keine benannten Ebenen unterstützen oder Eigenschaften elementweise speichern. Wenn die Eigenschaft für alle Elemente in einer Ebene gilt, ist diese Spalte **NULL**. Für Anbieter, die eindeutige Namen durch eine Einschränkung generieren, ist jede Komponente dieses Namens begrenzt.|  
|**PROPERTY_TYPE**|**DBTYPE_I2**||Eine Bitmap, die den Typ der Eigenschaft angibt:<br /><br /> **MDPROP_MEMBER** (**1**) bezeichnet eine Eigenschaft eines Elements. Diese Eigenschaft kann in der DIMENSION PROPERTIES-Klausel der SELECT-Anweisung verwendet werden.<br /><br /> **MDPROP_CELL** (**2**) bezeichnet eine Eigenschaft einer Zelle. Diese Eigenschaft kann in der CELL PROPERTIES-Klausel verwendet werden, die am Ende der SELECT-Anweisung vorkommt.<br /><br /> **MDPROP_SYSTEM** (**4**) gibt eine interne Eigenschaft.<br /><br /> **MDPROP_BLOB** (**8**) bezeichnet eine Eigenschaft, die ein binary large Object (Blob) enthält.|  
|**EIGENSCHAFTSNAME**|**DBTYPE_WSTR**||Der Name der Eigenschaft. Wenn der Schlüssel für die Eigenschaft identisch mit dem Namen für die Eigenschaft ist **PROPERTY_NAME** leer.|  
|**PROPERTY_CAPTION**|**DBTYPE_WSTR**||Eine der Eigenschaft zugeordnete Bezeichnung oder Beschriftung, die hauptsächlich zu Anzeigezwecken verwendet wird. Gibt **PROPERTY_NAME** Wenn keine Beschriftung vorhanden.|  
|**DATA_TYPE**|**DBTYPE_UI2**||Der Datentyp der Eigenschaft.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||Die maximal mögliche Länge der Eigenschaft, wenn es sich um einen Zeichen-, Binär- oder Bittyp handelt.<br /><br /> Null gibt an, dass es keine definierte maximale Länge gibt.<br /><br /> Gibt **NULL** für alle anderen Datentypen.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||Die maximal mögliche Länge der Eigenschaft (in Byte), wenn es sich um einen Zeichen- oder Binärtyp handelt.<br /><br /> Null gibt an, dass es keine definierte maximale Länge gibt.<br /><br /> Gibt **NULL** für alle anderen Datentypen.|  
|**"NUMERIC_PRECISION"**|**DBTYPE_UI2**||Die maximale Genauigkeit der Eigenschaft, wenn es sich um einen numerischen Datentyp handelt.<br /><br /> Gibt **NULL** für alle anderen Datentypen.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||Die Anzahl der Ziffern rechts vom Dezimaltrennzeichen, wird jedoch eine **DBTYPE_NUMERIC** oder **DBTYPE_DECIMAL** Typ.<br /><br /> Gibt **NULL** für alle anderen Datentypen.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine lesbare Beschreibung der Eigenschaft. **NULL** , wenn keine Beschreibung vorhanden ist.|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**||Der Typ der Eigenschaft. Dieser kann eine der folgenden Enumerationen sein:<br /><br /> **MD_PROPTYPE_REGULAR** (**0 x 00**)<br /><br /> **MD_PROPTYPE_ID** (**0 x 01**)<br /><br /> **MD_PROPTYPE_RELATION_TO_PARENT** (**0 x 02**)<br /><br /> **MD_PROPTYPE_ROLLUP_OPERATOR** (**0 x 03**)<br /><br /> **MD_PROPTYPE_ORG_TITLE** (**0x11**)<br /><br /> **MD_PROPTYPE_CAPTION** (**0 x 21**)<br /><br /> **MD_PROPTYPE_CAPTION_SHORT** (**0 x 22**)<br /><br /> **MD_PROPTYPE_CAPTION_DESCRIPTION** (**0 x 23**)<br /><br /> **MD_PROPTYPE_CAPTION_ABREVIATION** (**0 x 24**)<br /><br /> **MD_PROPTYPE_WEB_URL** (**0x31**)<br /><br /> **MD_PROPTYPE_WEB_HTML** (**0 x 32**)<br /><br /> **MD_PROPTYPE_WEB_XML_OR_XSL** (**0 x 33**)<br /><br /> **MD_PROPTYPE_WEB_MAIL_ALIAS** (**0 x 34**)<br /><br /> **MD_PROPTYPE_ADDRESS** (**0 x 41 nach**)<br /><br /> **MD_PROPTYPE_ADDRESS_STREET** (**0 x 42**)<br /><br /> **MD_PROPTYPE_ADDRESS_HOUSE** (**0x43**)<br /><br /> **MD_PROPTYPE_ADDRESS_CITY** (**0 x 44**)<br /><br /> **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (**0 x 45**)<br /><br /> **MD_PROPTYPE_ADDRESS_ZIP** (**0 x 46**)<br /><br /> **MD_PROPTYPE_ADDRESS_QUARTER** (**0x47**)<br /><br /> **MD_PROPTYPE_ADDRESS_COUNTRY** (**0 x 48**)<br /><br /> **MD_PROPTYPE_ADDRESS_BUILDING** (**0 x 49**)<br /><br /> **MD_PROPTYPE_ADDRESS_ROOM** (**0x4A**)<br /><br /> **MD_PROPTYPE_ADDRESS_FLOOR** (**0x4B**)<br /><br /> **MD_PROPTYPE_ADDRESS_FAX** (**0x4C**)<br /><br /> **MD_PROPTYPE_ADDRESS_PHONE** (**0x4D**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_X** (**0 x 61**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Y** (**0x62**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Z** (**0 x 63**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_TOP** (**0x64**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (**0x65**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (**0x66**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (**0 x 67**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (**0x68**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_REAR** (**0x69**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (**0x6A**)<br /><br /> **MD_PROPTYPE_PHYSICAL_SIZE** (**0x71**)<br /><br /> **MD_PROPTYPE_PHYSICAL_COLOR** (**0 x 72**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WEIGHT** (**0 x 73**)<br /><br /> **MD_PROPTYPE_PHYSICAL_HEIGHT** (**0 x 74**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WIDTH** (**0x75**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DEPTH** (**0x76**)<br /><br /> **MD_PROPTYPE_PHYSICAL_VOLUME** (**0 x 77**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DENSITY** (**0 x 78**)<br /><br /> **MD_PROPTYPE_PERSON_FULL_NAME** (**0 x 82**)<br /><br /> **MD_PROPTYPE_PERSON_FIRST_NAME** (**0 x 83**)<br /><br /> **MD_PROPTYPE_PERSON_LAST_NAME** (**0 x 84**)<br /><br /> **MD_PROPTYPE_PERSON_MIDDLE_NAME** (**0x85**)<br /><br /> **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (**0x86**)<br /><br /> **MD_PROPTYPE_PERSON_CONTACT** (**0x87**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_LOW** (**0 x 91**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_HIGH** (**0 x 92**)<br /><br /> **MD_PROPTYPE_FORMATTING_COLOR** (**0xA1**)<br /><br /> **MD_PROPTYPE_FORMATTING_ORDER** (**0xA2**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT** (**0xA3**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (**0xA4**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_SIZE** (**0xA5**)<br /><br /> **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (**0xA6**)<br /><br /> **MD_PROPTYPE_DATE** (**0xB1**)<br /><br /> **MD_PROPTYPE_DATE_START** (**0xB2**)<br /><br /> **MD_PROPTYPE_DATE_ENDED** (**0xB3**)<br /><br /> **MD_PROPTYPE_DATE_CANCELED** (**0xB4**)<br /><br /> **MD_PROPTYPE_DATE_MODIFIED** (**0xb5 festgelegt ist**)<br /><br /> **MD_PROPTYPE_DATE_DURATION** (**0xB6**)<br /><br /> **MD_PROPTYPE_VERSION** (**0xC1**)|  
|**SQL_COLUMN_NAME**|**DBTYPE_WSTR**||Der Name der Eigenschaft, die in SQL-Abfragen von der Cubedimension oder Datenbankdimension verwendet wird.|  
|**LANGUAGE**|**DBTYPE_UI2**||Die Übersetzung, ausgedrückt als eine **LCID**. Nur gültig für Eigenschaftenübersetzungen.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**||Gibt den Typ der Hierarchie an, für die die Eigenschaft gilt:<br /><br /> **MD_USER_DEFINED** (**1**) gibt an, dass die Eigenschaft auf eine benutzerdefinierte Hierarchie<br /><br /> **Md_system_enabled gültig** (**2**) gibt an, dass die Eigenschaft für eine Attributhierarchie gilt<br /><br /> **MD_SYSTEM_DISABLED** (**4**) gibt an, dass die Eigenschaft auf die Attributhierarchie nicht aktiviert ist.|  
|**PROPERTY_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**||Der Name der Attributhierarchie, die als Quelle für diese Eigenschaft dient.|  
|**PROPERTY_CARDINALITY**|**DBTYPE_WSTR**||Die Kardinalität der Eigenschaft. Die folgenden Zeichenfolgen sind möglich:<br /><br /> **EINE**<br /><br /> **VIELE**|  
|**MIME_TYPE**|**DBTYPE_WSTR**||Der MIME-Typ für Binary Large Objects (BLOBs).|  
|**PROPERTY_IS_VISIBLE**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob die Eigenschaft sichtbar ist.<br /><br /> **"True"** ist die Eigenschaft sichtbar ist, andernfalls **"false"**.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **MDSCHEMA_PROPERTIES** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Obligatorisch.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional|  
|**PROPERTY_TYPE**|**DBTYPE_I2**|Optional|  
|**EIGENSCHAFTSNAME**|**DBTYPE_WSTR**|Optional|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**|(Optional) Eine standardeinschränkung ist vorhanden, auf **MDPROP_MEMBER** oder **MDPROP_CELL**.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**|(Optional) Eine standardeinschränkung ist vorhanden, auf **MD_USER_DEFINED** oder **md_system_enabled gültig**.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1.  Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**PROPERTY_VISIBILITY**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> 1 Sichtbar<br /><br /> 2 Nicht sichtbar|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
