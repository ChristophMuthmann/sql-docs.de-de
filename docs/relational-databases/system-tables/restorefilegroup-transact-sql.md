---
title: Restorefilegroup (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- restorefilegroup_TSQL
- restorefilegroup
dev_langs: TSQL
helpviewer_keywords:
- filegroups [SQL Server], restorefilegroup system table
- restorefilegroup system table
ms.assetid: 3aa15c55-6b72-4f76-97d7-bd88391d105c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cbdf5074c50b2072ef60bdccb0541f4760bdd43
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="restorefilegroup-transact-sql"></a>restorefilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede wiederhergestellte Dateigruppe. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Eindeutiger Bezeichner, der den entsprechenden Wiederherstellungsvorgang angibt. Verweise **restorehistory(restore_history_id)**.|  
|**filegroup_name**|**vom Datentyp nvarchar(128)**|Name der wiederhergestellten Dateigruppe. Kann den Wert NULL haben.<br /><br /> Wird eine Datenbankmomentaufnahme einer Datenbank wiederhergestellt, wird dieser Wert auf die gleiche Weise wie bei einer vollständigen Wiederherstellung aufgefüllt.|  
  
## <a name="remarks"></a>Hinweise  
 Um die Anzahl der Zeilen in dieser Tabelle und in anderen Tabellen sicherungs- und Verlaufstabellen zu verringern, führen Sie die [Sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Tabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [Restorefile &#40; Transact-SQL &#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [Restorehistory &#40; Transact-SQL &#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
