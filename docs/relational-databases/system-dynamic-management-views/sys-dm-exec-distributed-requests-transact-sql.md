---
title: Sys.dm_exec_distributed_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 539bf6f6e4df5860977fdd0703a9bc11a5923d31
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>Sys.dm_exec_distributed_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Anforderungen, die zurzeit oder zuletzt aktiv in PolyBase-Abfragen. Eine Zeile pro Anforderung bzw. die Abfrage aufgeführt.  
  
 Basierend auf der Sitzung und Anforderungs-ID, ein Benutzer kann dann abrufen, die tatsächlichen verteilte-Anforderungen, die generiert wird, um über sys.dm_exec_distributed_requests – ausgeführt werden. Beispielsweise wird eine Abfrage, die im Zusammenhang mit regulären SQL und externe SQL-Tabellen in verschiedenen Anweisungen/ausgeführten Anforderungen, die über die verschiedenen Serverknoten zerlegt werden sollen. Um die verteilte Schritte auf allen Serverknoten nachzuverfolgen, führen wir eine "global" ausführungs-ID, der verwendet werden kann, um alle Vorgänge auf den Serverknoten, die eine bestimmte Anforderung und -Operator, jeweils zugeordneten nachzuverfolgen.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|Der Schlüssel für diese Ansicht. Eindeutige numerische Id der Anforderung zugeordnet ist.|Für alle Anforderungen im System eindeutig.|  
|execution_id|**nvarchar(32**|Eindeutige numerische Id der Sitzung, in der diese Abfrage ausgeführt wurde, zugeordnet.||  
|status|**nvarchar(32**|Aktueller Status der Anforderung.|"Ausstehend" fehlgeschlagen "Autorisieren", "AcquireSystemResources", "Initialisieren", "Planung", "Analysieren", "AquireResources", "Wird ausgeführt", "Abbrechen", "Vollständig","", "Abgebrochen".|  
|error_id|**nvarchar(36)**|Eindeutige Id des Fehlers mit der Anforderung verknüpft sind, sofern vorhanden.|Auf NULL festgelegt, wenn kein Fehler aufgetreten ist.|  
|start_time|**datetime**|Zeitpunkt, an dem die anforderungsausführung gestartet wurde.|für Anforderungen in der Warteschlange 0; andernfalls, gültige DateTime-Wert kleiner oder gleich der aktuellen Zeit.|  
|end_time|**datetime**|Zeitpunkt, an dem das Modul abgeschlossen Kompilieren die Anforderung.|NULL für in der Warteschlange "oder" aktiv Anforderungen. andernfalls einen gültigen DateTime-Wert kleiner oder gleich der aktuellen Zeit.|  
|total_elapsed_time|**int**|Bei der Ausführung verstrichene Zeit seit dem Start die Anforderung, in Millisekunden.|Zwischen 0 und der Unterschied zwischen Start_time und end_time des Intervalls. Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl überschreitet, weiterhin Total_elapsed_time der maximale Wert sein. Diese Bedingung generiert die Warnung "der maximale Wert überschritten wurde." Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
