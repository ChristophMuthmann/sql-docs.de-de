---
title: Sys.dm_pdw_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 381f23c5f72ab6e089a691850dab18b257f669be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>Sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen über alle Verteilungen von SQL Server-Abfrage als Teil eines SQL-Schritts in der Abfrage.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Eindeutiger Bezeichner der Abfrage zu der dieser SQL-Abfrage-Verteilung gehört.<br /><br /> Request_id Step_index und Distribution_id bilden den Schlüssel für diese Ansicht ein.|Finden Sie unter Request_id in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Der Index des Schritts Abfrage, die diesem Verteilungspunkt gehört.<br /><br /> Request_id Step_index und Distribution_id bilden den Schlüssel für diese Ansicht ein.|Finden Sie unter Step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**int**|Eindeutiger Bezeichner des Knotens, auf dem diese Verteilung von Abfragen ausgeführt wird.|Finden Sie unter "node_id" in [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**int**|Eindeutiger Bezeichner der Verteilung auf der diese Verteilung von Abfragen ausgeführt wird.<br /><br /> Request_id Step_index und Distribution_id bilden den Schlüssel für diese Ansicht ein.|Finden Sie unter Distribution_id in [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). -1 für die im Gültigkeitsbereich Knoten, nicht den Verteilungsbereich ausgeführten Anforderungen festgelegt ist.|  
|status|**nvarchar(32)**|Aktueller Status der Verteilung von Abfragen.|Ausstehend "" "ausgeführt", "fehlgeschlagen", "abgebrochen", "abgeschlossen", wurde abgebrochen, CancelSubmitted|  
|error_id|**nvarchar(36)**|Eindeutiger Bezeichner des Fehlers diese Verteilung von Abfragen, ggf. zugeordnet.|Finden Sie unter Fehler-ID in [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Auf NULL festgelegt, wenn kein Fehler aufgetreten ist.|  
|start_time|**datetime**|Zeitpunkt Verteilung mit der Ausführung begonnen hat.|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich Start_time des Schritts Abfrage gehört dieser Verteilung von Abfragen|  
|end_time|**datetime**|Zeitpunkt, zu dem diese Verteilung von Abfragen die Ausführung wurde abgeschlossen, wurde abgebrochen oder fehlerhaft.|Größer oder gleich Startzeit oder auf NULL festgelegt werden, wenn die Verteilung von Abfragen einer laufenden oder in der Warteschlange ist.|  
|total_elapsed_time|**int**|Stellt die Zeit, die die Verteilung von Abfragen, die in Millisekunden ausgeführt wurde.|Größer oder gleich 0. Gleich das Delta der Start_time und End_time für abgeschlossen, fehlgeschlagen ist oder abgebrochen Abfrage Verteilungen.<br /><br /> Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl überschreitet, weiterhin Total_elapsed_time der maximale Wert sein. Diese Bedingung generiert die Warnung "der maximale Wert überschritten wurde."<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
|row_count|**bigint**|Anzahl der Zeilen geändert oder von dieser Verteilung von Abfragen gelesen werden.|-1 für Vorgänge, die nicht ändern oder Daten, z. B. CREATE TABLE und DROP TABLE zurück.|  
|spid|**int**|Sitzungs-Id für die SQL Server-Instanz, die die Verteilung von Abfragen ausgeführt.||  
|Befehl|**nvarchar(4000)**|Vollständiger Text der Befehl für diese Verteilung von Abfragen.|Jede gültige Abfrage oder einen Anforderung-Zeichenfolge.|  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie im Abschnitt "maximale Systemwerte anzeigen" in der [Mindest- und Höchstwerte (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) Thema.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
