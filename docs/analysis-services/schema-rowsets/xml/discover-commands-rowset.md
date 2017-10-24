---
title: DISCOVER_COMMANDS-Rowset | Microsoft Docs
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
helpviewer_keywords:
- DISCOVER_COMMANDS rowset
ms.assetid: d228f265-05d9-4d2c-a622-44c73eab7a71
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49d95852f838c67a34e175ed160c6abdad93bd61
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discovercommands-rowset"></a>DISCOVER_COMMANDS-Rowset
  Stellt Ressourcenverwendungs- und Aktivitätsinformationen über die zurzeit ausgeführten oder zuletzt ausgeführten Befehle auf den offenen Verbindungen auf dem Server bereit.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_COMMANDS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**SESSION_SPID**|**DBTYPE_I4**|ja|Die Sitzungs-ID.|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||Die Anzahl der seit dem Start der Sitzung ausgeführten Befehle.|  
|**COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||Das Datum und die Uhrzeit, zu denen der letzte Befehl gestartet wurde, ausgedrückt als UTC-Zeit auf dem Server.|  
|**COMMAND_ELAPSED_TIME_MS**|**DBTYPE_I8**||Die seit dem Start des Befehls verstrichene Zeit in Millisekunden.|  
|**COMMAND_CPU_TIME_MS**|**DBTYPE_I8**||Die CPU-Zeit in Millisekunden, die seit dem Start der Befehlsausführung von dem Befehl beansprucht wurde.|  
|**COMMAND_READS**|**DBTYPE_I8**||Die akkumulierte Anzahl der seit dem Start des Befehls erfolgten Lesevorgänge auf dem Datenträger.|  
|**COMMAND_READ_KB**|**DBTYPE_I8**||Der akkumulierte Wert der seit dem Start des Befehls vom Datenträger gelesenen Daten in KB.|  
|**COMMAND_WRITES**|**DBTYPE_I8**||Die akkumulierte Anzahl der seit dem Start des Befehls erfolgten Schreibvorgänge auf dem Datenträger.|  
|**COMMAND_WRITE_KB**|**DBTYPE_I8**||Der akkumulierte Wert der seit dem Start des Befehls auf den Datenträger geschriebenen Daten in KB.|  
|**COMMAND_TEXT**|**DBTYPE_WSTR**||Der Befehlstext.|  
|**COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||UTC-Datum und -Zeit des Servers, zu denen der Befehl seine Ausführung beendet.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd34-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|Befehle|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

