---
title: Logmarkhistory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d4948a79bfd4b529b87cd0f5c223e302172a26a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede markierte Transaktion, für die ein Commit ausgeführt wurde. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Lokale Datenbank, in der die markierte Transaktion aufgetreten ist|  
|**mark_name**|**nvarchar(128)**|Vom Benutzer bereitgestellter Name für die markierte Transaktion|  
|**description**|**nvarchar(255)**|Vom Benutzer bereitgestellte Beschreibung für die markierte Transaktion Kann den Wert NULL haben.|  
|**user_name**|**nvarchar(128)**|Datenbank-Benutzername, der die markierte Transaktion durchgeführt hat. Kann den Wert NULL haben.|  
|**lsn**|**numeric(25,0)**|Protokollsequenznummer des Transaktionsdatensatzes, in dem die Markierung auftrat|  
|**mark_time**|**datetime**|Bestätigungszeitpunkt der markierten Transaktion (lokale Zeit)|  
  
## <a name="see-also"></a>Siehe auch  
 [Wiederherstellen einer Datenbank bis zu einer markierten Transaktion &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
