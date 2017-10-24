---
title: DISCOVER_TRACE_DEFINITION_PROVIDERINFO-Rowset | Microsoft Docs
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
ms.assetid: 8dda2ef7-202a-454b-93f9-a2b29c2d277c
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 76de6c69ebfa480c3ed401b1be1fb203bfe34bd0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discovertracedefinitionproviderinfo-rowset"></a>DISCOVER_TRACE_DEFINITION_PROVIDERINFO-Rowset
  Gibt grundlegende Informationen zum Ablaufverfolgungsanbieter zurück, beispielsweise dessen Name und Beschreibung.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_TRACE_DEFINITION_PROVIDERINFO** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**Daten**|**DBTYPE_WSTR**|ja|Enthält eine codierte XML-Zeichenfolge, die den Ablaufverfolgungsanbieter beschreibt, einschließlich Anbietername, Version, Buildnummer und Beschreibung.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|A07CCD1B-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|TraceDefinitionProviderInfo|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

