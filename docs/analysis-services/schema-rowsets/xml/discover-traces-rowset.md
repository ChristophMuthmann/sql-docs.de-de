---
title: DISCOVER_TRACES-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c79aa16cc7dc0d232c3acaa4407588932befc124
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="discovertraces-rowset"></a>DISCOVER_TRACES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Stellt Informationen über die derzeit aktiven Ablaufverfolgungen auf dem Server bereit.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_TRACES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**TraceID**|**DBTYPE_WSTR**|Die Ablaufverfolgungs-ID.|  
|**TraceName**|**DBTYPE_WSTR**|Der Ablaufverfolgungsname.|  
|**LogFileName**|**DBTYPE_WSTR**|Der Name der Ablaufverfolgungsprotokolldatei.|  
|**LogFileSize**|**DBTYPE_I4**|Die Größe der Ablaufverfolgungsprotokolldatei.|  
|**LogFileRollover**|**DBTYPE_BOOL**|true, um anzugeben, dass die Protokolldatei von neuem beginnen soll, andernfalls false.|  
|**AutoRestart**|**DBTYPE_BOOL**|true, um anzugeben, dass die automatische Neustartoption aktiviert ist; andernfalls false.|  
|**CreationTime**|**DBTYPE_TIME**|Datum und Uhrzeit der Erstellung der Ablaufverfolgung.|  
|**StopTime**|**DBTYPE_TIME**|Beendigungszeit der Ablaufverfolgung.|  
|**Typ**|**PF_DBTYPE_WSTR**|Der Typ der Ablaufverfolgung.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_TRACES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|**DBTYPE_I4**|Optional.|  
|**Typ**|WSTR|Optional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
