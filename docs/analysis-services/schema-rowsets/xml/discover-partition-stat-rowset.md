---
title: DISCOVER_PARTITION_STAT-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0863c2f263cc13ff9673063ab1f49535cd2407a3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT-Rowset
  Gibt Statistiken zu Aggregationen in einer bestimmten Partition zurück.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_PARTITION_STAT** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATENBANKNAME**|**DBTYPE_WSTR**|Required|Der Name der Datenbank, welche die Dimension enthält.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Required|Der Namen des Cubes oder des Tabellenmodells mit der Partition.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Required|Der Name der Measuregruppe in der Dimension.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**PARTITIONSNAME**|**DBTYPE_WSTR**|Required|Der Name einer Partition.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**AGGREGATION_NAME**|**DBTYPE_WSTR**||Der Name der Aggregation.|  
|**AGGREGATION_SIZE**|**DBTYPE_I8**||Die Größe der Aggregation.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

