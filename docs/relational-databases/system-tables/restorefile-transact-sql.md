---
title: Restorefile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59e6f1c08440f2053c8f3d4bc3a74f0dcfd60ef3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede wiederhergestellte Datei. Dies gilt auch für Dateien, die indirekt nach Dateigruppennamen wiederhergestellt werden. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Eindeutiger Bezeichner, der den entsprechenden Wiederherstellungsvorgang angibt. Verweise **restorehistory(restore_history_id)**.|  
|**file_number**|**numeric(10,0)**|Datei-ID der wiederhergestellten Datei. Diese Nummer muss in jeder Datenbank eindeutig sein. Kann den Wert NULL haben.<br /><br /> Wird eine Datenbankmomentaufnahme einer Datenbank wiederhergestellt, wird dieser Wert auf die gleiche Weise wie bei einer vollständigen Wiederherstellung aufgefüllt.|  
|**destination_phys_drive**|**nvarchar(260)**|Laufwerk oder Partition, in welche(s) die Datei wiederhergestellt wurde. Kann den Wert NULL haben.<br /><br /> Wird eine Datenbankmomentaufnahme einer Datenbank wiederhergestellt, wird dieser Wert auf die gleiche Weise wie bei einer vollständigen Wiederherstellung aufgefüllt.|  
|**destination_phys_name**|**nvarchar(260)**|Name der Datei, in welche die Datei wiederhergestellt wurde, ohne die Informationen zu Laufwerk oder Partition. Kann den Wert NULL haben.<br /><br /> Wird eine Datenbankmomentaufnahme einer Datenbank wiederhergestellt, wird dieser Wert auf die gleiche Weise wie bei einer vollständigen Wiederherstellung aufgefüllt.|  
  
## <a name="remarks"></a>Hinweise  
 Um die Anzahl der Zeilen in dieser Tabelle und in anderen Tabellen sicherungs- und Verlaufstabellen zu verringern, führen Sie die [Sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Tabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
