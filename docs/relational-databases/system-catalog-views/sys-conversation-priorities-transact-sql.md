---
title: Sys. conversation_priorities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- conversation_priorities_TSQL
- conversation_priorities
- sys.conversation_priorities_TSQL
- sys.conversation_priorities
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], priorities
- Service Broker, conversations
- sys.conversation_priorities catalog view
ms.assetid: 7cbb9171-3310-4aae-8458-755c882d6462
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73d823e5ad3efb2b91f4a0fd591d4e3fa54eefd5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysconversationpriorities-transact-sql"></a>sys.conversation_priorities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede in der aktuellen Datenbank erstellte Konversationspriorität, wie in der folgenden Tabelle gezeigt wird: 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|Priority_id|**int**|Eine Zahl, die die Konversationspriorität eindeutig identifiziert. Lässt keine NULL-Werte zu.|  
|name|**sysname**|Der Name der Konversationspriorität. Lässt keine NULL-Werte zu.|  
|service_contract_id|**int**|Der Bezeichner des Vertrags, der für die Konversationspriorität angegeben ist. Dieser kann mit der service_contract_id-Spalte in sys.service_contracts verknüpft werden. Lässt NULL-Werte zu.|  
|local_service_id|**int**|Der Bezeichner des Diensts, der als lokaler Dienst für die Konversationspriorität angegeben ist. Diese Spalte kann mit der service_id-Spalte in  sys.services verknüpft werden. Lässt NULL-Werte zu.|  
|remote_service_name|**nvarchar(256)**|Der Name des Diensts, der als Remotedienst für die Konversationspriorität angegeben ist. Lässt NULL-Werte zu.|  
|priority|**tinyint**|Die Prioritätsebene, die in dieser Konversationspriorität angegeben ist. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Konversationsprioritäten aufgeführt. Mithilfe von Joins werden dabei der Name des Vertrags und des lokalen Diensts angezeigt.  
  
```  
SELECT scp.name AS priority_name,  
       ssc.name AS contract_name,  
       ssvc.name AS local_service_name,  
       scp.remote_service_name,  
       scp.priority AS priority_level  
FROM sys.conversation_priorities AS scp  
    INNER JOIN sys.service_contracts AS ssc  
       ON scp.service_contract_id = ssc.service_contract_id  
    INNER JOIN sys.services AS ssvc  
       ON scp.local_service_id = ssvc.service_id  
ORDER BY priority_name, contract_name,  
         local_service_name, remote_service_name;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.services &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)   
 [sys.service_contracts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-contracts-transact-sql.md)  
  
  
