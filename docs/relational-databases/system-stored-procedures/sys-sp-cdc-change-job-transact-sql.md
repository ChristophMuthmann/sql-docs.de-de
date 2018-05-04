---
title: sp_cdc_change_job (Transact-SQL) | Microsoft Docs
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
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4878eeca70732ed5a7ab19e220eac60260e71ee9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Konfiguration eines Cleanup- oder Aufzeichnungsauftrags für Change Data Capture in der aktuellen Datenbank. Um die aktuelle Konfiguration eines Auftrags anzuzeigen, Fragen Sie die [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) -Tabelle ab, oder verwenden Sie [Sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_type=** ] **"***Job_type***"**  
 Der Typ des zu ändernden Auftrags. *Der Standardwert ist* ist **nvarchar(20)** hat den Standardwert 'Capture'. Gültige Eingaben sind 'capture' und 'cleanup'.  
  
 [ **@maxtrans** ] **= *** Max_trans*  
 Maximale Anzahl der in jedem Scanzyklus zu verarbeitenden Transaktionen. *Max_trans* ist **Int** hat den Standardwert NULL, gibt für diesen Parameter keine Änderung vorliegt. Wenn dieser Wert angegeben ist, muss er eine positive ganze Zahl annehmen.  
  
 *Max_trans* ist nur für aufzeichnungsaufträge gültig.  
  
 [ **@maxscans** ] **= *** Max_scans*  
 Maximale Anzahl der Scanzyklen, die ausgeführt werden sollen, um alle Zeilen aus dem Protokoll zu extrahieren. *Max_scans* ist **Int** hat den Standardwert NULL, gibt für diesen Parameter keine Änderung vorliegt.  
  
 *Max_scan* ist nur für aufzeichnungsaufträge gültig.  
  
 [ **@continuous** ] **= *** fortlaufende*  
 Gibt an, ob der Aufzeichnungsauftrag kontinuierlich (1) oder nur einmal (0) ausgeführt wird. *kontinuierliche* ist **Bit** hat den Standardwert NULL, gibt für diesen Parameter keine Änderung vorliegt.  
  
 Wenn *fortlaufende* = 1, der [Sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) Auftrag überprüft das Protokoll und verarbeitet bis zu (*Max_trans* \* *Max_scans*) Transaktionen. Er wartet dann die Anzahl der Sekunden, die im angegebenen *Polling_interval* vor Beginn des nächsten protokollscans.  
  
 Wenn *fortlaufende* = 0, die **Sp_cdc_scan** Auftrag ausführt, bis zu *Max_scans* Scanvorgänge des Protokolls, verarbeitet dabei bis zu *Max_trans* Transaktionen während jedes Scanvorgangs und wird dann beendet.  
  
 Wenn **@continuous** von 1 in 0 geändert wird **@pollinginterval** automatisch auf 0 festgelegt ist. Ein Wert für angegeben **@pollinginterval** abgesehen 0 ignoriert wird.  
  
 Wenn **@continuous** weggelassen oder explizit auf NULL gesetzt und **@pollinginterval** wird explizit auf einen Wert größer 0 festgelegt, **@continuous** automatisch auf 1 festgelegt.  
  
 *fortlaufende* ist nur für aufzeichnungsaufträge gültig.  
  
 [ **@pollinginterval** ] **= *** Polling_interval*  
 Anzahl der Sekunden zwischen Protokollscan navigieren. *Polling_interval* ist **"bigint"** hat den Standardwert NULL, gibt für diesen Parameter keine Änderung vorliegt.  
  
 *Polling_interval* ist nur für aufzeichnungsaufträge gültig Wenn Aufträge *fortlaufende* auf 1 festgelegt ist.  
  
 [ **@retention** ] **= *** Aufbewahrung*  
 Die Anzahl von Minuten, für die Änderungszeilen in Änderungstabellen beibehalten werden sollen. *Aufbewahrung* ist **"bigint"** hat den Standardwert NULL, gibt für diesen Parameter keine Änderung vorliegt. Der Maximalwert beträgt 52494800 (100 Jahre). Wenn dieser Wert angegeben ist, muss er eine positive ganze Zahl annehmen.  
  
 *Aufbewahrung* ist nur für cleanupaufträge gültig.  
  
 [  **@threshold=** ] **"***löschen Schwellenwert***"**  
 Maximale Anzahl von Einträgen für Löschvorgänge, die mit einer einzelnen Anweisung beim Cleanup gelöscht werden können. *Löschen von Schwellenwert* ist **"bigint"** hat den Standardwert NULL, gibt für diesen Parameter keine Änderung vorliegt. *Löschen von Schwellenwert* ist nur für cleanupaufträge gültig.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Parameter weggelassen, wird der zugeordnete Wert in der [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) Tabelle wird nicht aktualisiert. Ein explizit auf NULL festgelegter Parameter wird so behandelt, als ob der Parameter weggelassen wird.  
  
 Die Angabe eines für den Auftragstyp ungültigen Parameters führt dazu, dass die Anweisung fehlschlägt.  
  
 Änderungen an einem Auftrag werden wirksam, bis der Auftrag beendet wird, mithilfe von [Sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) und über [Sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_owner** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-a-capture-job"></a>A. Ändern eines Aufzeichnungsauftrags  
 Das folgende Beispiel aktualisiert die `@job_type`, `@maxscans`, und `@maxtrans` Parameter eines aufzeichnungsauftrags in der `AdventureWorks2012` Datenbank. Die anderen gültigen Parameter für einen Aufzeichnungsauftrag, `@continuous` und `@pollinginterval`, werden weggelassen. Deren Werte werden nicht geändert.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>B. Ändern eines Cleanupauftrags  
 Im folgenden Beispiel wird ein Cleanupauftrag in der `AdventureWorks2012`-Datenbank aktualisiert. Alle gültigen Parameter für diesen Auftragstyp, außer **@threshold**, angegeben werden. Der Wert der **@threshold** wird nicht geändert.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sp_cdc_add_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
