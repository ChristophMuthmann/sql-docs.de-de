---
title: MDSCHEMA_CUBES-Rowset | Microsoft Docs
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
- MDSCHEMA_CUBES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f56517d3f8a974ae54d08f0dda2c24de5025facb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Beschreibt die Struktur der Cubes innerhalb einer Datenbank.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **MDSCHEMA_CUBES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Der Name der Datenbank.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Nicht unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Der Name des Cubes oder der Dimension. Dimensionsnamen ist ein Dollarzeichensymbol ($) vorangestellt.<br /><br /> Hinweis: Nur Server- und Datenbankadministratoren haben Berechtigungen zum Anzeigen von Cubes, die aus einer Dimension erstellt wurden.|  
|**CUBE_TYPE**|**DBTYPE_WSTR**|Der Typ des Cubes. Gültige Werte sind:<br /><br /> **CUBE**<br /><br /> **DIMENSION**|  
|**CUBE_GUID**|**DBTYPE_GUID**|Nicht unterstützt.|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**|Nicht unterstützt.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**|Der Zeitpunkt der letzten Verarbeitung des Cubes.|  
|**SCHEMA_UPDATED_BY**|**DBTYPE_WSTR**|Nicht unterstützt.|  
|**LAST_DATA_UPDATE**|**DBTYPE_DBTIMESTAMP**|Der Zeitpunkt der letzten Verarbeitung des Cubes.|  
|**DATA_UPDATED_BY**|**DBTYPE_WSTR**|Nicht unterstützt.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine benutzerfreundliche Beschreibung des Cubes.|  
|**IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|Ein boolescher Wert, der immer True zurückgibt.|  
|**IS_LINKABLE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob ein Cube in einem verknüpften Cube verwendet werden kann.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob für einen Cube der Schreibzugriff aktiviert ist.|  
|**IS_SQL_ENABLED**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob SQL für den Cube verwendet werden kann.|  
|**CUBE_CAPTION**|**DBTYPE_WSTR**|Die Beschriftung des Cubes.|  
|**BASE_CUBE_NAME**|**DBTYPE_WSTR**|Der Name des Quellcubes, wenn dieser Cube ein perspektivischer Cube ist.|  
|**ANMERKUNGEN**|**DBTYPE_WSTR**|(Optional) Ein Satz von Hinweisen im XML-Format.|  
  
 Das Rowset wird sortiert nach **CATALOG_NAME**, **SCHEMA_NAME**und **CUBE_NAME**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **MDSCHEMA_CUBES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden gültigen Werte:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**Basis Cube_Name**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
