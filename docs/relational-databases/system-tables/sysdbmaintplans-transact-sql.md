---
title: Sysdbmaintplans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b8639b05e8e87e58d2e70e9cf240d3ee161f35b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Tabelle dient in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beibehalten der vorhandenen Informationen für Instanzen, die von einer früheren Version von aktualisiert [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ändert den Inhalt dieser Tabelle nicht. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID des Datenbankwartungsplans.|  
|**plan_name**|**sysname**|Name des Datenbankwartungsplans.|  
|**date_created**|**datetime**|Erstellungsdatum des Datenbankwartungsplans.|  
|**Besitzer**|**sysname**|Besitzer des Datenbankwartungsplans.|  
|**max_history_rows**|**int**|Maximale Anzahl von Zeilen, die für das Aufzeichnen des Verlaufs für den Datenbankwartungsplan in der Systemtabelle zugeteilt werden.|  
|**remote_history_server**|**sysname**|Der Name des Remoteservers, auf den der Verlaufsbericht geschrieben werden konnte.|  
|**max_remote_history_rows**|**int**|Maximale Anzahl von Zeilen, die in der Systemtabelle auf einem Remoteserver zugeteilt wurden und in die der Verlaufsbericht geschrieben werden konnte.|  
|**user_defined_1**|**int**|Der Standardwert ist NULL.|  
|**user_defined_2**|**Nvarchar(100)**|Der Standardwert ist NULL.|  
|**user_defined_3**|**datetime**|Der Standardwert ist NULL.|  
|**user_defined_4**|**uniqueidentifier**|Der Standardwert ist NULL.|  
|**log_shipping**|**bit**|Protokollversandstatus:<br /><br /> **0** = Deaktiviert **1** = Aktiviert|  
  
  
