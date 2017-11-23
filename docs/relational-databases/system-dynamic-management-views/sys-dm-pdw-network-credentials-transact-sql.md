---
title: Sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
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
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21935bde6ebefe2b30743a4961ba05e3092539d6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>Sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Gibt eine Liste aller Netzwerkanmeldeinformationen, in gespeichert der [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance für alle Zielserver. Für den Knoten, und jeder Serverknoten sind die Ergebnisse aufgeführt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|Eindeutige numerische Id, die dem Knoten zugeordnet.|  
|target_server_name|**nvarchar(32)**|IP-Adresse des Zielservers, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] greifen mithilfe der Anmeldeinformationen für Benutzername und Kennwort.|  
|username|**nvarchar(32)**|Der Benutzername für die das Kennwort gespeichert wird.|  
|last_modified|**datetime**|DateTime-Wert des letzten Vorgangs, der die Anmeldeinformationen geändert.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Der Schlüssel für diese dynamische verwaltungssicht ist *Pdw_node_id* plus *Target_server_name*.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
