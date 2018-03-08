---
title: sys.service_contract_message_usages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea323e7e57da5f2bb9fb3930d2de3fb5289759b9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysservicecontractmessageusages-transact-sql"></a>sys.service_contract_message_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Katalogsicht enthält eine Zeile pro Vertrag/Nachrichtentyp-Paar.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|Bezeichner des Vertrags, der den Nachrichtentyp verwendet. Lässt keine NULL-Werte zu.|  
|**message_type_id**|**int**|Bezeichner des Nachrichtentyps, der vom Vertrag verwendet wird. Lässt keine NULL-Werte zu.|  
|**is_sent_by_initiator**|**bit**|Der Nachrichtentyp kann vom Konversationsinitiator gesendet werden. Lässt keine NULL-Werte zu.|  
|**is_sent_by_target**|**bit**|Der Nachrichtentyp kann vom Konversationsziel gesendet werden. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
