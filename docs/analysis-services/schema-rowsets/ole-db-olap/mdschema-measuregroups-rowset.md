---
title: MDSCHEMA_MEASUREGROUPS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: MDSCHEMA_MEASUREGROUPS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 470a0987e6bc23b9b2d85283bfb85866036cec5d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Beschreibt die Measuregruppen innerhalb einer Datenbank.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **MDSCHEMA_MEASUREGROUPS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||Der Name des Katalogs, zu dem diese Measuregruppe gehört. **NULL** , wenn der Anbieter keine Kataloge unterstützt.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Nicht unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Der Name des Cubes, zu dem diese Measuregruppe gehört.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||Der Name der Measuregruppe.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine lesbare Beschreibung des Elements.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob der Schreibzugriff für die Measuregruppe aktiviert ist.<br /><br /> Gibt **true** zurück, wenn der Schreibzugriff für die Measuregruppe aktiviert ist.|  
|**MEASUREGROUP_CAPTION**|**DBTYPE_WSTR**||Die Anzeigebeschriftung für die Measuregruppe.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **MDSCHEMA_MEASUREGROUPS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
