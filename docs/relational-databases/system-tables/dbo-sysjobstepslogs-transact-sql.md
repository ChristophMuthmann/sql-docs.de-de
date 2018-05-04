---
title: dbo.sysjobstepslogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 791f23f988dcd74ed39dba95a1f3f22efa818f9b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält das auftragsschrittprotokoll für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftragsschritten, die zum Schreiben der Ausgabe des Auftragsschritts in eine Tabelle konfiguriert sind. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|ID des Auftragsschrittprotokolls.|  
|**log**|**nvarchar(max)**|Inhalt des Auftragsschrittprotokolls.|  
|**date_created**|**datetime**|Datum und Uhrzeit der Erstellung des Auftragsschrittprotokolls.|  
|**date_modified**|**datetime**|Datum und Uhrzeit der letzten Änderung des Auftragsschrittprotokolls.|  
|**log_size**|**int**|Größe des Auftragsschrittprotokolls in Bytes.|  
|**step_uid**|**uniqueidentifier**|Eindeutiger Bezeichner des Auftragsschrittes.|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
