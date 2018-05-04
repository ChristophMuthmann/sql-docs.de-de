---
title: DBSCHEMA_TABLES-Rowset | Microsoft Docs
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
- DBSCHEMA_TABLES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1e6117a2a17457a919e202a6dfeef411a766e0f3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dbschematables-rowset"></a>DBSCHEMA_TABLES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt die Measuregruppen und Dimensionen, die in als Tabellen verfügbar gemacht [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DBSCHEMA_TABLES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|255|Der Name des Katalogs, zu dem dieses Objekt gehört.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|255|Der Name des Cubes, zu dem dieses Objekt gehört.|  
|**TABLE_NAME**|**DBTYPE_WSTR**|255|Der Name des Objekts, wenn **TABLE_TYPE** **TABLE**lautet.|  
|**TABLE_TYPE**|**DBTYPE_WSTR**||Der Typ der Tabelle.<br /><br /> **TABLE** gibt an, dass das Objekt eine Measuregruppe ist.<br /><br /> **SYSTEM TABLE** gibt an, dass das Objekt eine Dimension ist.|  
|**TABLE_GUID**|**DBTYPE_GUID**||Nicht unterstützt.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine lesbare Beschreibung des Objekts.|  
|**TABLE_PROPID**|**DBTYPE_UI4**||Nicht unterstützt.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||Nicht unterstützt.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Das Datum, an dem das Objekt zuletzt geändert wurde.|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**||Den OLAP-Typ des Objekts.<br /><br /> **MEASURE_GROUP** gibt an, dass das Objekt eine Measuregruppe ist.<br /><br /> **CUBE_DIMENSION** gibt an, dass das Objekt eine Dimension ist.|  
  
 Das Rowset wird sortiert nach **TABLE_TYPE**, **TABLE_CATALOG**, **TABLE_SCHEMA**und **TABLE_NAME**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DBSCHEMA_TABLES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|Optional|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|Optional|  
|**TABLE_NAME**|**DBTYPE_WSTR**|Optional|  
|**TABLE_TYPE**|**DBTYPE_WSTR**|Optional|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**|Optional|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
