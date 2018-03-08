---
title: Sys. transmission_queue (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8bfb955b7d44733d93379b999aca8b6267b28976
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="systransmissionqueue-transact-sql"></a>sys.transmission_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Katalogsicht enthält eine Zeile für jede Nachricht in der Übertragungswarteschlange, wie in der folgenden Tabelle gezeigt wird.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|Bezeichner für die Konversation, zu der diese Nachricht gehört. Lässt keine NULL-Werte zu.|  
|**to_service_name**|**nvarchar(256)**|Name des Diensts, an den diese Nachricht gerichtet ist. Lässt NULL-Werte zu.|  
|**to_broker_instance**|**nvarchar(128)**|Bezeichner des Brokers, der den Dienst hostet, an den diese Nachricht gerichtet ist. Lässt NULL-Werte zu.|  
|**from_service_name**|**nvarchar(256)**|Name des Diensts, von dem diese Nachricht stammt. Lässt NULL-Werte zu.|  
|**service_contract_name**|**nvarchar(256)**|Name des Vertrags, dem die Konversation für diese Nachricht entspricht. Lässt NULL-Werte zu.|  
|**enqueue_time**|**datetime**|Zeitpunkt, zu dem die Nachricht der Warteschlange hinzugefügt wurde. Dieser Wert verwendet die UTC-Zeit unabhängig von der lokalen Zeitzone für die Instanz. Lässt keine NULL-Werte zu.|  
|**message_sequence_number**|**bigint**|Sequenznummer der Nachricht. Lässt keine NULL-Werte zu.|  
|**message_type_name**|**nvarchar(256)**|Name des Nachrichtentyps für die Nachricht. Lässt NULL-Werte zu.|  
|**is_conversation_error**|**bit**|Gibt an, ob diese Nachricht eine Fehlermeldung ist.<br /><br /> 0 = Keine Fehlermeldung.<br /><br /> 1 = Fehlermeldung.<br /><br /> Lässt keine NULL-Werte zu.|  
|**is_end_of_dialog**|**bit**|Gibt an, ob diese Nachricht das Ende der Konversationsnachricht ist. Lässt keine NULL-Werte zu.<br /><br /> 0 = Kein Ende der Konversationsnachricht.<br /><br /> 1 = Ende der Konversationsnachricht.<br /><br /> Lässt keine NULL-Werte zu.|  
|**message_body**|**varbinary(max)**|Der Nachrichtentext. Lässt NULL-Werte zu.|  
|**transmission_status**|**nvarchar(4000)**|Der Grund, weshalb sich diese Nachricht in der Warteschlange befindet. Dies ist im Allgemeinen eine Fehlermeldung, mit der erläutert wird, weshalb beim Senden der Nachricht ein Fehler aufgetreten ist. Wenn dieses Feld leer ist, wurde die Nachricht noch nicht gesendet. Lässt NULL-Werte zu.|  
|**priority**|**tinyint**|Die Prioritätsebene, die der Nachricht zugewiesen wird. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
