---
title: Sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.reviewer: 
ms.service: 
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffd9bad344ed79048a65de4139ec7c2fd44cd9c4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>Sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Enthält Informationen zu den verschiedenen Windows-Ereignis auf den anderen Knoten protokolliert.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Appliance-Knoten, die dieses Protokoll stammt.<br /><br /> Pdw_node_id und Log_name bilden den Schlüssel für diese Ansicht ein.||  
|log_name|**nvarchar(255)**|Name des Windows-Ereignisprotokoll.<br /><br /> Pdw_node_id und Log_name bilden den Schlüssel für diese Ansicht ein.||  
|log_source|**nvarchar(255)**|Quellenname für Windows-Ereignisprotokoll.||  
|event_id|**int**|Die ID des Ereignisses. Nicht eindeutig.||  
|event_type|**nvarchar(255)**|Der Typ des Ereignisses, Schweregrad identifizieren.|"Information", "Warnung", "Fehler"|  
|event_message|**nvarchar(4000)**|Die Details des Ereignisses.||  
|generate_time|**datetime**|Zeitpunkt, zu das Ereignis erstellt wurde.||  
|write_time|**datetime**|Uhrzeit, die das Ereignis tatsächlich in das Protokoll geschrieben wurde.||  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie im Abschnitt "maximale Systemwerte anzeigen" in der [Mindest- und Höchstwerte (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) Thema.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
