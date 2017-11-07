---
title: DBSCHEMA_COLUMNS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DBSCHEMA_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 93cd52a3f37c9e14af6132708fd36591ac846f59
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS-Rowset
  Stellt Spalteninformationen für alle Spalten bereit, die den bereitgestellten Einschränkungskriterien entsprechen.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DBSCHEMA_COLUMNS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**"TABLE_CATALOG"**|**DBTYPE_WSTR**||Der Name der Datenbank.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**TABELLENNAME**|**DBTYPE_WSTR**||Der Name des Cubes.|  
|**SPALTENNAME**|**DBTYPE_WSTR**||Der Name der Attributhierarchie oder des Measures.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||Wird nicht unterstützt.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||Wird nicht unterstützt.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||Die Position der Spalte, beginnend mit 1.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**||Wird nicht unterstützt.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||Eine **DBCOLUMNFLAGS** -Bitmaske, die die Spalteneigenschaften angibt. Siehe "DBCOLUMNFLAGS Enumerated Type" in [IColumnsInfo::GetColumnInfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||Gibt immer **false**zurück.|  
|**DATA_TYPE**|**DBTYPE_WSTR**<br /><br /> **DBTYPE_VARIANT**||Der Datentyp der Spalte. Gibt eine Zeichenfolge für Dimensionsspalten und eine Variante für Measures zurück.|  
|**TYPE_GUID**|**DBTYPE_GUID**||Wird nicht unterstützt.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||Die maximal mögliche Länge eines Werts in der Spalte.<br /><br /> Dieser Wert wird von der **DataSize** -Eigenschaft in **DataItem**abgerufen.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||Die maximal mögliche Länge eines Werts in der Spalte in Bytes für Zeichen- oder Binärspalten.<br /><br /> Der Wert null (0) gibt an, dass die Spalte keine maximale Länge besitzt.<br /><br /> Für Spalten, die keine Binär- oder Zeichendatentypen zurückgeben, wird**NULL** zurückgegeben.|  
|**"NUMERIC_PRECISION"**|**DBTYPE_UI2**||Die maximale Genauigkeit der Spalte für andere numerische Datentypen als **DBTYPE_VARNUMERIC**.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||Die Anzahl der Stellen rechts neben dem Dezimalzeichen für **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**und **DBTYPE_VARNUMERIC**. Andernfalls ist der Wert **NULL**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||Wird nicht unterstützt.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**SORTIERUNGSNAME**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**DOMÄNENNAME**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Wird nicht unterstützt.|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**||Den OLAP-Typ des Objekts.<br /><br /> **MEASURE** gibt an, dass das Objekt ein Measure ist.<br /><br /> **ATTRIBUTE** gibt an, dass das Objekt ein Dimensionsattribut ist.<br /><br /> **SCHEMA** gibt an, dass das Objekt eine Spalte in einem Schema ist.|  
  
 Das Rowset wird sortiert nach **TABLE_CATALOG**, **TABLE_SCHEMA**und **TABLE_NAME**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DBSCHEMA_COLUMNS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**"TABLE_CATALOG"**|**DBTYPE_WSTR**|Optional|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|Optional|  
|**TABELLENNAME**|**DBTYPE_WSTR**|Optional|  
|**SPALTENNAME**|**DBTYPE_WSTR**|Optional|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**|Optional|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

