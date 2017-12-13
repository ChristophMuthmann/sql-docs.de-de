---
title: DISCOVER_DIMENSION_STAT-Rowset | Microsoft Docs
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
applies_to: SQL Server 2016 Preview
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bfe9352a73c2548bfa092eb88d04605b6721b4ed
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="discoverdimensionstat-rowset"></a>DISCOVER_DIMENSION_STAT-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Enthält Informationen zu einer Dimension, einschließlich des Namens der Datenbank, die es, den Dimensionsnamen, ihre Attribute und eine Anzahl der Elemente für jedes Attribut enthält. In einem tabellarischen Modell entspricht dies den Spalten in einer Tabelle und der Anzahl von Werten in jeder Spalte.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_DIMENSION_STAT** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATENBANKNAME**|**DBTYPE_WSTR**|Required|Der Name der Datenbank, welche die Dimension enthält.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|Required|Der Name der Dimension.<br /><br /> Diese Spalte ist in der Einschränkungsliste erforderlich.|  
|**ATTRIBUTNAME**|**DBTYPE_WSTR**||Der Name eines Attributs in der Dimension.|  
|**ATTRIBUTE_COUNT**|**DBTYPE_I8**||Die Anzahl der Werte im benannten Attribut. Für ein tabellarisches Modell entspricht der Wert immer der Anzahl der Zeilen in der Tabelle.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis – Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
