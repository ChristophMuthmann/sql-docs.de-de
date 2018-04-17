---
title: dbo.systargetservers (Transact-SQL) | Microsoft Docs
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
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1fcce3f0020036cc0a0d21021be24dcdcd8ab19a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeichnet auf, welche Zielserver derzeit in dieser Domäne für Multiservervorgänge eingetragen sind.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Server-ID.|  
|**server_name**|**sysname**|Servername.|  
|**location**|**nvarchar(200)**|Speicherort des angegebenen Zielservers.|  
|**time_zone_adjustment**|**int**|Zeitanpassungsintervall in Bezug auf die GMT (Greenwich Mean Time) in Stunden.|  
|**enlist_date**|**datetime**|Datum und Uhrzeit der Eintragung des angegebenen Zielservers.|  
|**last_poll_date**|**datetime**|Datum und Uhrzeit des Zeitpunkts, an dem der angegebene Zielserver die **sysdownloadlist** -Systemtabelle des Multiservers zuletzt abgerufen hat, um nach auszuführenden Aufträgen zu suchen.|  
|**status**|**int**|Status des Zielservers:<br /><br /> **1** = Normal<br /><br /> **2** = Neusynchronisierung ausstehend<br /><br /> **4** = Offline vermutet|  
|**local_time_at_last_poll**|**datetime**|Datum und Uhrzeit des letzten Versuchs, Auftragsvorgänge vom Zielserver abzurufen.|  
|**enlisted_by_nt_user**|**Nvarchar(100)**|Benutzername der Person, die **sp_msx_enlist** auf dem Zielserver ausführt.|  
|**poll_internal**|**int**|Anzahl von Sekunden, die verstreichen müssen, bevor der Zielserver versucht, vom Masterserver neue Downloadanweisungen abzurufen.|  
  
  
