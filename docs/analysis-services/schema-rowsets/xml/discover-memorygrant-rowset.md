---
title: DISCOVER_MEMORYGRANT-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba8bbb7752557c845899c587a39c9ceef357d578
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discovermemorygrant-rowset"></a>DISCOVER_MEMORYGRANT-Rowset
  Gibt eine Liste interner Arbeitsspeicherkontingent-Erteilungen zurück, die von Aufträgen in Anspruch genommen werden, die derzeit auf dem Server ausgeführt werden. Um festzustellen, ob ein Auftrag auf dem Server ausgeführt wird, verwenden Sie `Select * from $System.Discover_Jobs`.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_MEMORYGRANT** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MEMORY_ID**|**DBTYPE_I8**||Eine Zahl, die die Arbeitsspeicherkontingent-Zuweisung identifiziert. Eindeutig innerhalb des Kontexts einer einzelnen DISCOVER_MEMORYGRANT-Anforderung.|  
|**SPID**|**DBTYPE_I4**|Required|Die SPID, die Sie erhalten können, indem Sie `Select * from $System.Discover_Sessions`ausführen.|  
|**CreationTime**|**DBTYPE_I8 DBTYPE_DBTIMESTAMP**||Die Uhrzeit, zu der das Kontingent zugewiesen wurde.|  
|**LastRequestTime**|**DBTYPE_DBTIMESTAMP**||Die Uhrzeit, zu der die Kontingentanforderung zuletzt geändert wurde.|  
|**MemoryUsed**|**DBTYPE_I4**||Der im Zusammenhang mit dem Kontingent verwendete Arbeitsspeicher.|  
|**MemoryGranted**|**DBTYPE_I4**||Der zur Verwendung durch den Auftrag, der das Arbeitsspeicherkontingent abruft, zugewiesene Arbeitsspeicher.|  
|**Blockiert**|**DBTYPE_BOOL**||Ein boolescher Wert, der den Blockstatus des Auftrags angibt. True gibt an, dass der Auftrag blockiert wurde, bis ein anderer Auftrag genügend Kontingent freigibt, um seine Kontingentanforderung zu gewähren. False gibt an, dass der Auftrag sein Kontingent empfangen hat und ausgeführt werden kann.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

