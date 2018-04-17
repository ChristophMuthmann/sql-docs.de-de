---
title: dm_broker_forwarded_messages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6314f4c69d2744b3d25917f01ee1a5d2ae29edd8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmbrokerforwardedmessages-transact-sql"></a>sys.dm_broker_forwarded_messages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Service Broker-Nachricht, die eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird gerade weiterleiten.  
  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|ID der Konversation, zu der diese Nachricht gehört. Lässt NULL-Werte zu.|  
|**is_initiator**|**bit**|Gibt an, ob diese Nachricht vom Initiator der Konversation stammt.  Lässt NULL-Werte zu.<br /><br /> 0 = Nicht vom Initiator<br /><br /> 1 = Vom Initiator|  
|**to_service_name**|**nvarchar(512)**|Name des Diensts, an den diese Nachricht gesendet wird. Lässt NULL-Werte zu.|  
|**to_broker_instance**|**nvarchar(512)**|Bezeichner des Brokers, der als Host für den Dienst dient, an den diese Nachricht gesendet wird. Lässt NULL-Werte zu.|  
|**from_service_name**|**nvarchar(512)**|Name des Diensts, von dem diese Nachricht stammt. Lässt NULL-Werte zu.|  
|**from_broker_instance**|**nvarchar(512)**|Bezeichner des Brokers, der als Host für den Dienst dient, von dem diese Nachricht stammt. Lässt NULL-Werte zu.|  
|**adjacent_broker_address**|**nvarchar(512)**|Netzwerkadresse, an die diese Nachricht gesendet wird. Lässt NULL-Werte zu.|  
|**message_sequence_number**|**bigint**|Sequenznummer der Nachricht im Dialogfeld. Lässt NULL-Werte zu.|  
|**message_fragment_number**|**int**|Bei Fragmentierung der Dialognachricht ist dies die Fragmentnummer, die diese Transportnachricht enthält. Lässt NULL-Werte zu.|  
|**hops_remaining**|**tinyint**|Häufigkeit, mit der die Nachricht erneut übertragen werden kann, bevor sie das endgültige Ziel erreicht. Bei jeder Weiterleitung der Nachricht nimmt diese Zahl um 1 ab. Lässt NULL-Werte zu.|  
|**time_to_live**|**int**|Maximal verbleibende Zeit, die die Nachricht aktiviert bleiben kann. Wird der Wert 0 erreicht, wird die Nachricht verworfen. Lässt NULL-Werte zu.|  
|**time_consumed**|**int**|Zeitdauer der bisherigen Aktivität der Nachricht. Bei jeder Weiterleitung der Nachricht steigt diese Zahl um die Zeitdauer, die die Weiterleitung der Nachricht benötigt hat. Lässt keine NULL-Werte zu.|  
|**message_id**|**uniqueidentifier**|ID der Meldung. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Verbindung mit Service Broker dynamische Verwaltungssichten & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

