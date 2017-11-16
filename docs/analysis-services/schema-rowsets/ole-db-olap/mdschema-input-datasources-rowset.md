---
title: MDSCHEMA_INPUT_DATASOURCES-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname:
- MDSCHEMA_INPUT_DATASOURCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e105cc8151640f5d5d74d6c7c76cc52edc16a242
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemainputdatasources-rowset"></a>MDSCHEMA_INPUT_DATASOURCES-Rowset
  Beschreibt die innerhalb der Datenbank definierten Datenquellen.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **MDSCHEMA_INPUT_DATASOURCES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||Der Name des Katalogs, zu dem diese Datenquelle gehört.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**%{DATASOURCE_NAME/}-DATENQUELLE**|**DBTYPE_WSTR**||Der Name des Datenquellenobjekts.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**||Der Typ der Datenquelle. Gültige Werte sind:<br /><br /> **Relationale**<br /><br /> **OLAP**|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**||Das Datum, an dem die Datenquelle erstellt wurde.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**||Das Datum und die Uhrzeit der letzten Änderung der Datenquelle.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine benutzerfreundliche Beschreibung der Aktion.|  
|**TIMEOUT**|**DBTYPE_UI4**||Das Timeout der Datenquelle.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **MDSCHEMA_INPUT_DATASOURCES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**%{DATASOURCE_NAME/}-DATENQUELLE**|**DBTYPE_WSTR**|Optional.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

