---
title: DISCOVER_STORAGE_TABLES-Rowset | Microsoft Docs
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
applies_to: SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ceaff6d458686f33a7e32126f3f46c1e5675b144
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="discoverstoragetables-rowset"></a>DISCOVER_STORAGE_TABLES-Rowset
  Ermöglicht dem Client, die Tabellen zu bestimmen, die in einer im tabellarischen Modus oder SharePoint-Modus ausgeführten Analysis Services-Datenbank enthalten sind.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_STORAGE_TABLES** -Rowset enthält die folgenden Spalten.  
  
|**Spaltenname**|**Typindikator**|**Länge**|**Description**|  
|---------------------|------------------------|----------------|---------------------|  
|**DATENBANKNAME**|**DBTYPE_WSTR**||Gibt den Namen der Datenbank an, die die Tabellen enthält.<br /><br /> Das **DISCOVER_STORAGE_TABLES** -Rowset kann mithilfe dieser Spalte eingeschränkt werden. Wenn diese Spalte nicht verwendet wird, um das Rowset einzuschränken, wird die aktuelle Datenbank verwendet.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Gibt den Cube oder das Modell an, das die Tabellen enthält.<br /><br /> Das **DISCOVER_STORAGE_TABLES** -Rowset kann mithilfe dieser Spalte eingeschränkt werden.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||Der Name der Measuregruppe.|  
|**PARTITIONSNAME**|**DBTYPE_WSTR**||Der Name der Partition.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Der Name der Dimension.|  
|**TABLE_ID**|**DBTYPE_WSTR**||Die ID der Tabelle, die verwendet wird, um die Tabellenattribute zu speichern.|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE_ WSTR**||Die Anzahl der Tabellenpartitionen.|  
|**HINT_TABLE_TYPE**|**DBTYPE_ WSTR**||Der Hinweis auf den Tabellentyp.|  
|**ROWS_COUNT**|**DBTYPE_UI4**||Anzahl der Zeilen in der Partition.|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||Die Anzahl der Zeilen mit Verstößen gegen die referenzielle Integrität.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_STORAGE_TABLES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|**Spaltenname**|**Typindikator**|**Einschränkungsstatus**|  
|---------------------|------------------------|---------------------------|  
|**DATENBANKNAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Optional|  
|**PARTITIONSNAME**|**DBTYPE_WSTR**|Optional|  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird von der Standarddatenbank der aktuellen Verbindung eine Liste der Speichertabellen und die Anzahl der darin jeweils enthaltenen Zeilen zurückgegeben.  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
