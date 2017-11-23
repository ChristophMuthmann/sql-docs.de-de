---
title: DISCOVER_PARTITION_DIMENSION_STAT-Rowset | Microsoft Docs
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
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eb81657e74e36f6a854b1bca22a1e61b44cde693
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="discoverpartitiondimensionstat-rowset"></a>DISCOVER_PARTITION_DIMENSION_STAT-Rowset
  Gibt Statistiken zur Dimension zurück, die einer Partition zugeordnet ist.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_PARTITION_DIMENSION_STAT** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATENBANKNAME**|**DBTYPE_WSTR**|Required|Der Name der Datenbank.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Required|Der Namen des Cubes oder des Tabellenmodells.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Required|Der Name der Measuregruppe.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**PARTITIONSNAME**|**DBTYPE_WSTR**|Required|Der Name der Partition.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Der Name der Dimension.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**ATTRIBUTNAME**|**DBTYPE_WSTR**||Der Name eines Attributs in der Dimension.|  
|**ATTRIBUTE_INDEXED**|**DBTYPE_BOOL**||true, um anzugeben, dass das Attribut indiziert ist; andernfalls false.|  
|**ATTRIBUTE_COUNT_MIN**|**DBTYPE_I8**||Mindestanzahl für das Attribut.|  
|**ATTRIBUTE_COUNT_MAX**|**DBTYPE_I8**||Maximale Anzahl für das Attribut.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis – Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
