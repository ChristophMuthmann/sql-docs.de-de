---
title: Sys. dm_filestream_file_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_file_io_requests
- dm_filestream_file_io_requests
- sys.dm_filestream_file_io_requests_TSQL
- dm_filestream_file_io_requests_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_filestream_file_io_requests catalog view
ms.assetid: d41e39a5-14d5-4f3d-a2e3-a822b454c1ed
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4ae89e50f6afaab2d84f8c7adb4cc0b0f3144df
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmfilestreamfileiorequests-transact-sql"></a>sys.dm_filestream_file_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt eine Liste mit E/A-Anforderungen an, die im betreffenden Moment vom Namespace-Besitzer (NSO) verarbeitet werden.  
  
|Column|Typ|Description|  
|------------|----------|-----------------|  
|**request_context_address**|**varbinary(8)**|Zeigt die interne Adresse des NSO-Speicherblocks an, der die E/A-Anforderung des Treibers enthält. Lässt keine NULL-Werte zu.|  
|**current_spid**|**smallint**|Zeigt die Systemprozess-ID (SPID) für die aktuelle Verbindung des SQL Servers an. Lässt keine NULL-Werte zu.|  
|**request_type**|**nvarchar(60)**|Zeigt den Typ des E/A-Anforderungspakets (IRP) an. Die möglichen Anforderungstypen sind REQ_PRE_CREATE, REQ_POST_CREATE, REQ_RESOLVE_VOLUME, REQ_GET_VOLUME_INFO, REQ_GET_LOGICAL_NAME, REQ_GET_PHYSICAL_NAME, REQ_PRE_CLEANUP, REQ_POST_CLEANUP, REQ_CLOSE, REQ_FSCTL, REQ_QUERY_INFO, REQ_SET_INFO, REQ_ENUM_DIRECTORY, REQ_QUERY_SECURITY und REQ_SET_SECURITY. Lässt keine NULL-Werte zu.|  
|**request_state**|**nvarchar(60)**|Zeigt den Status der E/A-Anforderung in NSO an. Mögliche Werte sind REQ_STATE_RECEIVED, REQ_STATE_INITIALIZED, REQ_STATE_ENQUEUED, REQ_STATE_PROCESSING, REQ_STATE_FORMATTING_RESPONSE, REQ_STATE_SENDING_RESPONSE, REQ_STATE_COMPLETING und REQ_STATE_COMPLETED. Lässt keine NULL-Werte zu.|  
|**request_id**|**int**|Zeigt die eindeutige Anforderungs-ID an, die der Anforderung vom Treiber zugewiesen ist. Lässt keine NULL-Werte zu.|  
|**irp_id**|**int**|Zeigt die eindeutige IRP-ID an. Dies ist zur Ermittlung aller E/A-Anforderungen hilfreich, die mit der vorliegenden IRP in Verbindung stehen. Lässt keine NULL-Werte zu.|  
|**handle_id**|**int**|Gibt die Handle-ID für den Namespace an. Dies ist der NSO-spezifische Bezeichner und in einer Instanz eindeutig. Lässt keine NULL-Werte zu.|  
|**client_thread_id**|**varbinary(8)**|Zeigt die Thread-ID der Clientanwendung an, von der die Anforderung gestartet wird.<br /><br /> **\*\*Warnung \* \***  Dies ist nur sinnvoll, wenn die Clientanwendung auf dem gleichen Computer wie SQL Server ausgeführt wird. Wird die Clientanwendung remote ausgeführt, zeigt die **client_thread_id** die Thread-ID eines Systemprozesses an, der für den Remoteclient ausgeführt wird.<br /><br /> Lässt NULL-Werte zu.|  
|**client_process_id**|**varbinary(8)**|Zeigt die Prozess-ID der Clientanwendung an, wenn die Clientanwendung auf dem gleichen Computer wie SQL Server ausgeführt wird. Im Falle eines Remoteclients wird die Systemprozess-ID angezeigt, die für die Clientanwendung angezeigt wird. Lässt NULL-Werte zu.|  
|**handle_context_address**|**varbinary(8)**|Zeigt die Adresse der internen NSO-Struktur an, die der Handle des Clients zugeordnet ist. Lässt NULL-Werte zu.|  
|**filestream_transaction_id**|**varbinary(128)**|Zeigt die ID der Transaktion an, die der vorliegenden Handle und allen dieser Handle zugeordneten Anforderungen zugeordnet ist. Hierbei handelt es sich um den Wert, der von der **get_filestream_transaction_context** -Funktion zurückgegeben wird. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [FileStream und FileTable dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
