---
title: DISCOVER_TRANSACTIONS-Rowset | Microsoft Docs
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
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a9dc8533965c6187311cedbecafb6361e5f505a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="discovertransactions-rowset"></a>DISCOVER_TRANSACTIONS-Rowset
  Gibt den aktuellen Satz von ausstehenden Transaktionen auf dem System zurück.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_TRANSACTIONS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**AKTIVIERT**|**DBTYPE_WSTR**|Der eindeutige Bezeichner der Transaktion als GUID.|  
|**TRANSACTION_SESSION_ID**|**DBTYPE_WSTR**|Die eindeutige Sitzungs-ID der Transaktion als GUID.|  
|**TRANSACTION_START_TIME**|**DBTYPE_DBTIMESTAMP**|UTC-Datum und -Zeit des Servers, zu denen die Transaktion gestartet wurde.|  
|**TRANSACTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|Die seit dem Start der Transaktion verstrichene Zeit in Millisekunden.|  
|**TRANSACTION_CPU_TIME_MS**|**DBTYPE_I8**|Die CPU-Zeit in Millisekunden, die seit dem Beginn der Transaktion von allen Anforderungen beansprucht wurde.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_TRANSACTIONS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|**Spaltenname**|**Typindikator**|**Einschränkungsstatus**|  
|---------------------|------------------------|---------------------------|  
|**ID**|**DBTYPE_WSTR**|Optional.|  
|**SESSION_ID**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis – Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
