---
title: Sys.dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 95e5165f7194e02374753443bd9a7ef120709b4c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>Sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Systemsicht, die Informationen über alle Daten Bewegung Service (DMS) Schritte für externe Vorgänge enthält.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Abfrage, die dieser Arbeitsthread DMS verwendet wird.<br /><br /> Request_id Step_index und Dms_step_index bilden den Schlüssel für diese Ansicht ein.|Identisch mit Request_id in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Abfrageschritt, die dieser Arbeitsthread DMS aufruft.<br /><br /> Request_id Step_index und Dms_step_index bilden den Schlüssel für diese Ansicht ein.|Identisch mit Step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Aktuelle Schritt im Plan DMS.<br /><br /> Request_id Step_index und Dms_step_index bilden den Schlüssel für diese Ansicht ein.|Identisch mit Dms___step_index in [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Knoten, der den DMS-Worker ausgeführt wird.|Identisch mit "node_id" in [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|Typ|**nvarchar(60)**|Typ des externen Vorgang, der diesem Knoten ausgeführt wird.<br /><br /> AUFTEILEN der Datei ist ein Vorgang auf einer externen Hadoop-Datei, die in mehrere kleinere greift aufgeteilt wurde.|"DATEI SPLIT"|  
|work_id|**int**|Die Datei aufteilen ID.|Größer als oder gleich 0.<br /><br /> Jede Serverknoten eindeutig.|  
|input_name|**nvarchar(60)**|Name für die gelesene Eingabe eine Zeichenfolge.|Für einen Hadoop-Dateien ist dies der Name der Hadoop-Datei.|  
|read_location|**bigint**|Offset der schreibgeschützten Speicherort.||  
|estimated_bytes_processed|**bigint**|Anzahl der Bytes, die von diesem Arbeitsthread verarbeitet werden.|Größer als oder gleich 0.|  
|length|**bigint**|Teilen Sie die Anzahl der Bytes in der Datei.<br /><br /> Für Hadoop ist dies die Größe des HDFS-Blocks.|Benutzerdefiniert. Der Standardwert beträgt 64 MB.|  
|status|**nvarchar(32)**|Status des Arbeitsthreads.|Wartet auf und Verarbeiten von Arbeit, Fehler, abgebrochen|  
|start_time|**datetime**|Zeitpunkt, zu dem Ausführung dieses Arbeitsthreads begonnen hat.|Größer als oder gleich der Startzeit des Schritts Abfrage wird dieser Arbeitsthread angehört. Finden Sie unter [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Uhrzeit der Ausführung beendet wurde, ist fehlgeschlagen, oder wurde abgebrochen.|NULL für laufende oder in der Warteschlange Worker. Andernfalls, Start_time größer.|  
|total_elapsed_time|**int**|Gesamtzeit für die Ausführung in Millisekunden.|Größer als oder gleich 0.<br /><br /> Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl überschreitet, weiterhin Total_elapsed_time der maximale Wert sein. Diese Bedingung generiert die Warnung "der maximale Wert überschritten wurde."<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie unter [maximale Systemwerte Ansicht](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
