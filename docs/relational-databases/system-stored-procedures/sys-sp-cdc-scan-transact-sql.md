---
title: sp_cdc_scan (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8cd29ff4ce371f6d893ceb396bb3a69d20bcab2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysspcdcscan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt den Protokollscan für Change Data Capture aus.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@maxtrans=** ] *Max_trans*  
 Maximale Anzahl der in jedem Scanzyklus zu verarbeitenden Transaktionen. *Max_trans* ist **Int** hat den Standardwert von 500.  
  
 [  **@maxscans=** ] *Max_scans*  
 Maximale Anzahl der Scanzyklen, die ausgeführt werden sollen, um alle Zeilen aus dem Protokoll zu extrahieren. *Max_scans* ist **Int** hat den Standardwert 10.  
  
 [  **@continuous=** ] *fortlaufende*  
 Gibt an, ob die gespeicherte Prozedur sollte beenden nach der Ausführung eines einzelnen Scanzyklus (0) oder kontinuierlich für die angegebene Zeit *Polling_interval* vor reexecuting der Überprüfungszyklus (1). *kontinuierliche* ist **"tinyint"** hat den Standardwert 0.  
  
 [  **@pollinginterval=** ] *Polling_interval*  
 Anzahl der Sekunden zwischen Protokollscan navigieren. *Polling_interval* ist **"bigint"** hat den Standardwert 0.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 sp_cdc_scan wird von sys.sp_MScdc_capture_job intern aufgerufen, wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-aufzeichnungsauftrag von Change Data Capture verwendet wird. Die Prozedur kann nicht explizit ausgeführt werden, wenn ein Protokollscan für Change Data Capture bereits aktiv ist oder wenn die Datenbank für die Transaktionsreplikation aktiviert ist. Diese gespeicherte Prozedur sollte von Administratoren verwendet werden, die das Verhalten von Capture-Auftrag, die automatisch konfiguriert wird, angepasst werden soll.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle "db_owner".  
  
## <a name="see-also"></a>Siehe auch  
 [cdc_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
