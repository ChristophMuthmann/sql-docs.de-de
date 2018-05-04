---
title: MDSCHEMA_DIMENSIONS-Rowset | Microsoft Docs
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
- MDSCHEMA_DIMENSIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c2561c27de11ad00541e7b0f3d582c84eb89ec1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Beschreibt die freigegebenen und privaten Dimensionen innerhalb einer Datenbank.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **MDSCHEMA_DIMENSIONS** Rowset enthält die folgenden Spalten:  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Der Name der Datenbank.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Nicht unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Der Name des Cubes.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|Der Name der Dimension. Wenn eine Dimension Teil mehrerer Cubes oder Measuregruppen ist, dann ist für jede eindeutige Kombination aus Dimension, Measuregruppe und Cube eine Zeile vorhanden.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Der eindeutige Name der Dimension.|  
|**DIMENSION_GUID**|**DBTYPE_GUID**|Nicht unterstützt.|  
|**DIMENSION_CAPTION**|**DBTYPE_WSTR**|Die Beschriftung der Dimension. Diese sollte verwendet werden, wenn dem Benutzer der Name der Dimension angezeigt wird, beispielsweise in der Benutzeroberfläche oder in Berichten.|  
|**DIMENSION_ORDINAL**|**DBTYPE_UI4**|Die Position der Dimension innerhalb des Cubes.|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|Der Typ der Dimension. Gültige Werte sind:<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**DIMENSION_CARDINALITY**|**DBTYPE_UI4**|Die Anzahl der Elemente im Schlüsselattribut.|  
|**DEFAULT_HIERARCHY**|**DBTYPE_WSTR**|Eine Hierarchie aus der Dimension. Dieser Parameter wird aus Gründen der Abwärtskompatibilität beibehalten.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine benutzerfreundliche Beschreibung der Dimension.|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|Immer **"false"**.|  
|**IS_READWRITE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob der Schreibzugriff für die Dimension aktiviert ist.<br /><br /> **"True"** , wenn die Dimension mit aktiviertem Schreibzugriff ist.|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|Eine Bitmap, die angibt, welche Spalten eindeutige Werte enthalten, wenn die Dimension nur Elemente mit eindeutigen Namen enthält. Die folgenden Bitwertkonstanten sind in der Datei Msmd.h für diese Bitmap definiert:<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE**|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|Immer **NULL**.|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|Immer **"true"**.<br /><br /> Hinweis: Eine Dimension ist nicht sichtbar, es sei denn, eine oder mehrere Hierarchien in der Dimension sichtbar sind.|  
  
 Das Rowset wird sortiert nach **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_NAME**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **MDSCHEMA_DIMENSIONS** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|Optional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> 1 Sichtbar<br /><br /> 2 Nicht sichtbar|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
