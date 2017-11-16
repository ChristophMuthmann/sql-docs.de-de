---
title: DISCOVER_MEMORYUSAGE-Rowset | Microsoft Docs
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: e416ea61-9615-468c-a96f-bbf731f803b1
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3dcbb314e1816757562f93290d95a3f9e345460b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discovermemoryusage-rowset"></a>DISCOVER_MEMORYUSAGE-Rowset
  Gibt die DISCOVER_MEMORYUSAGE-Statistiken für verschiedene vom Server zugeordnete Objekte zurück.  
  
> [!WARNING]  
>  Dieses Rowset kann sehr große Resultsets erzeugen. Wenn die Ergebnisse nicht angezeigt werden können, da sie mehr Anzeigearbeitsspeicher benötigen, als SQL Server Management Studio zulässt, werden die Ergebnisse am folgenden Standardspeicherort in eine temporäre Datei geschrieben:  
>   
>  "\<Laufwerk >: \Users\\< Benutzername\>\AppData\Local\Temp\\< FileID\>.xml".  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **DISCOVER_MEMORYUSAGE** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MemoryID**|**DBTYPE_UI8**||Eine Zahl, die den Arbeitsspeicher identifiziert.|  
|**MemoryName**|**DBTYPE_WSTR**||Der Name des Objekts, das den Arbeitsspeicher besitzt.|  
|**SPID**|**DBTYPE_UI4**|ja|Die Sitzung, die den Speicher zugewiesen hat. 0 (null) gibt an, dass der Arbeitsspeicher nicht an eine bestimmte Sitzung gebunden ist.|  
|**CreationTime**|**DBTYPE_DBTIMESTAMP**||Entweder "Uhrzeit der Erstellung des Objekts" oder "Zeitpunkt der Zuweisung des Speichers".|  
|**BaseObjectType**|**DBTYPE_UI4**|ja|Dies ist eine Zahl, die den Typ des Objekts beschreibt. Objekte mit demselben BaseObjectType haben denselben Typ.|  
|**MemoryUsed**|**DBTYPE_UI8**|ja|Dies ist die aktuelle Größe des Objekts, die möglicherweise geringer ist, als der zur Verwendung durch das Objekt zugeordnete Arbeitsspeicher.|  
|**MemoryAllocated**|**DBTYPE_UI8**||Die Menge des zur Verwendung durch das Objekt zugeordneten Arbeitsspeichers, die größer sein kann als der tatsächlich vom Objekt verwendete Arbeitsspeicher.|  
|**MemoryAllocBase**|**DBTYPE_UI8**||Die anfänglich für das Objekt (ohne zusätzliche Zuordnungen für Objektinhalt) zugeordneten Bytes.|  
|**MemoryAllocFromAlloc**|**DBTYPE_UI8**||Der für den Inhalt dieses Objekts zugewiesene Arbeitsspeicher.|  
|**ElementCount**|**DBTYPE_UI4**||Für ein Containerobjekt ist dies die Anzahl der in diesem Objekt enthaltenen Objekte.|  
|**Verkleinerung**|**DBTYPE_BOOL**|ja|Ein boolescher Wert, der angibt, wenn der Arbeitsspeicher verkleinerbar ist (kann aufgrund von ungenügend Arbeitsspeicher wegfallen). true, wenn der Arbeitsspeicher verkleinerbar ist; false, wenn der Arbeitsspeicher nicht verkleinerbar ist.|  
|**ObjectParentPath**|**DBTYPE_WSTR**||Eine Zeichenfolge, die den vollständigen Pfad dieses Objekts identifiziert.|  
|**ObjectID**|**DBTYPE_WSTR**||Die Zeichenfolge, die das Objekt identifiziert. Der vollständige Pfad dieses Objekts wird von der Zeichenfolge dargestellt: (ObjectParentPath + '.' + ObjectId).|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|A07CCD21-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|MemoryUsage|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

