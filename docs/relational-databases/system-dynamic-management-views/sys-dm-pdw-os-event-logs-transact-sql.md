---
title: Sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.service: ''
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a9876192ba5ce4a518401e4143f3365b10bfd913
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
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
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
