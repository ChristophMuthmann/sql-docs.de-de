---
title: sp_cdc_help_jobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_jobs
- sys.sp_cdc_help_jobs_TSQL
- sp_cdc_help_jobs_TSQL
- sys.sp_cdc_help_jobs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_help_jobs
ms.assetid: 9399b4bc-8293-408f-b3cb-f904e0657fb5
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f085c591fa0c417974f15244f8d9af39101fcc35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysspcdchelpjobs-transact-sql"></a>sys.sp_cdc_help_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen über alle Cleanup- oder Aufzeichnungsaufträge für Change Data Capture in der aktuellen Datenbank bereit.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_help_jobs  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Die ID des Auftrags.|  
|**Der Standardwert ist**|**nvarchar(20)**|Typ des Auftrags.|  
|**maxtrans**|**int**|Die maximale Anzahl der in jedem Scanzyklus zu verarbeitenden Transaktionen.<br /><br /> **Maxtrans** ist nur für aufzeichnungsaufträge gültig.|  
|**maxscans**|**int**|Die maximale Anzahl der scanzyklen, ausführen, um alle Zeilen aus dem Protokoll zu extrahieren.<br /><br /> **Maxscans** ist nur für aufzeichnungsaufträge gültig.|  
|**Fortlaufende**|**bit**|Flag, das angibt, ob der Aufzeichnungsauftrag fortlaufend (1) oder einmalig (0) ausgeführt werden soll. Weitere Informationen finden Sie unter [sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).<br /><br /> **fortlaufende** ist nur für aufzeichnungsaufträge gültig.|  
|**PollingInterval**|**bigint**|Anzahl der Sekunden zwischen Protokollscanzyklen.<br /><br /> **PollingInterval** ist nur für aufzeichnungsaufträge gültig.|  
|**Beibehaltungsdauer**|**bigint**|Anzahl der Minuten, die Änderungszeilen in Änderungstabellen beibehalten werden sollen.<br /><br /> **Aufbewahrung** ist nur für cleanupaufträge gültig.|  
|**threshold**|**bigint**|Die maximale Anzahl von Einträgen für Löschvorgänge, die mit einer einzelnen Anweisung beim Cleanup gelöscht werden können.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_owner** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zu den definierten Aufzeichnungs- und Cleanupaufträgen für die `AdventureWorks2012`-Datenbank zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_help_jobs;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_add_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
