---
title: Sys. dm_cdc_log_scan_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_cdc_log_scan_sessions
- dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions
dev_langs: TSQL
helpviewer_keywords:
- change data capture [SQL Server], log scan reporting
- sys.dm_cdc_log_scan_sessions dynamic management view
ms.assetid: d337e9d0-78b1-4a07-8820-2027d0b9f87c
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6db4f34391cf36757ed086b24ddfe3618ebbe529
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="change-data-capture---sysdmcdclogscansessions"></a>Change Data Capture - Sys. dm_cdc_log_scan_sessions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Protokollscansitzung in der aktuellen Datenbank zurück. Die letzte zurückgegebene Zeile stellt die aktuelle Sitzung dar. Mithilfe dieser Sicht können Sie Statusinformationen zur aktuellen Protokollscansitzung oder aggregierte Informationen zu allen Sitzungen zurückzugeben, seit die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das letzte Mal gestartet wurde.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID der Sitzung.<br /><br /> 0 = Die in dieser Zeile zurückgegebenen Daten sind ein Aggregat aller Sitzungen, seit die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das letzte Mal gestartet wurde.|  
|**start_time**|**datetime**|Zeitpunkt, zu dem die Sitzung begonnen wurde.<br /><br /> Wenn **Session_id** = 0, der Zeitpunkt, der aggregierten Datensammlung begonnen wurde.|  
|**end_time**|**datetime**|Zeitpunkt, zu dem die Sitzung beendet wurde.<br /><br /> NULL = Sitzung ist aktiv.<br /><br /> Wenn **Session_id** = 0, der Zeitpunkt der letzten Sitzung wurde beendet.|  
|**duration**|**bigint**|Die Dauer (in Sekunden) der Sitzung.<br /><br /> 0 = Die Sitzung enthält keine Change Data Capture-Transaktionen.<br /><br /> Wenn **Session_id** = 0, die Summer der Dauer (in Sekunden) aller Sitzungen mit Change Data Capture-Transaktionen.|  
|**scan_phase**|**nvarchar(200)-Datentyp gepackt ist**|Die aktuelle Phase der Sitzung. Im folgenden sind die möglichen Werte und deren Beschreibungen:<br /><br /> 1: Lesen der Konfiguration<br />2: ersten Scan, Erstellen der Hashtabelle<br />3: zweiter scan<br />4: zweiter scan<br />5: zweiter scan<br />6: versionsverwaltung des Schemas<br />7: der letzten Überprüfung<br />8: Fertig<br /><br /> Wenn **Session_id** = 0, ist der Wert immer "Aggregate".|  
|**error_count**|**int**|Anzahl der aufgetretenen Fehler.<br /><br /> Wenn **Session_id** = 0, die Gesamtanzahl der Fehler in allen Sitzungen.|  
|**start_lsn**|**nvarchar(23)**|Start-LSN für die Sitzung.<br /><br /> Wenn **Session_id** = 0, die Start-LSN für die letzte Sitzung.|  
|**current_lsn**|**nvarchar(23)**|Aktuelle LSN, die gescannt wird.<br /><br /> Wenn **Session_id** = 0, die aktuelle LSN ist 0.|  
|**end_lsn**|**nvarchar(23)**|Letzte LSN für die Sitzung.<br /><br /> NULL = Sitzung ist aktiv.<br /><br /> Wenn **Session_id** = 0, die letzte LSN für die letzte Sitzung.|  
|**tran_count**|**bigint**|Anzahl der verarbeiteten Change Data Capture-Transaktionen. Dieser Leistungsindikator wird in Phase 2 aufgefüllt.<br /><br /> Wenn **Session_id** = 0, die Anzahl der verarbeiteten Transaktionen in allen Sitzungen.|  
|**last_commit_lsn**|**nvarchar(23)**|LSN des letzten verarbeiteten Protokolldatensatzes für den Commit.<br /><br /> Wenn **Session_id** = 0, den letzten Commit Protokolldatensatz für jede andere Sitzung.|  
|**last_commit_time**|**datetime**|Zeitpunkt, zu dem der letzte Protokolldatensatz für den Commit verarbeitet wurde.<br /><br /> Wenn **Session_id** = 0, den Zeitpunkt das letzten Commit Protokolldatensatz für jede andere Sitzung.|  
|**log_record_count**|**bigint**|Anzahl der gescannten Protokolldatensätze.<br /><br /> Wenn **Session_id** = 0, Anzahl der gescannten Datensätze für alle Sitzungen.|  
|**schema_change_count**|**int**|Anzahl der erkannten Vorgänge in der Datendefinitionssprache (Data Definition Language, DDL). Dieser Leistungsindikator wird in Phase 6 aufgefüllt.<br /><br /> Wenn **Session_id** = 0, die Anzahl der DDL-Vorgänge, die in allen Sitzungen verarbeitet.|  
|**command_count**|**bigint**|Anzahl der verarbeiteten Befehle.<br /><br /> Wenn **Session_id** = 0, die Anzahl der Befehle, die in allen Sitzungen verarbeitet.|  
|**first_begin_cdc_lsn**|**nvarchar(23)**|Erste LSN, die Change Data Capture-Transaktionen enthalten hat.<br /><br /> Wenn **Session_id** = 0, die erste LSN, die Change Data Capture-Transaktionen enthalten.|  
|**last_commit_cdc_lsn**|**nvarchar(23)**|LSN des letzten Protokolldatensatzes für den Commit, der Change Data Capture-Transaktionen enthalten hat.<br /><br /> Wenn **Session_id** = 0 (null) der letzten Commitprotokolleintrag LSN für eine beliebige Sitzung enthaltenen Data Capture-Transaktionen Change|  
|**last_commit_cdc_time**|**datetime**|Zeitpunkt, zu dem der letzte Protokolldatensatz für den Commit verarbeitet wurde, der Change Data Capture-Transaktionen enthalten hat.<br /><br /> Wenn **Session_id** = 0, den Zeitpunkt der letzten Commit Protokolldatensatzes für den eine beliebige Sitzung change enthaltenen Data Capture-Transaktionen.|  
|**Latenz**|**int**|Der Unterschied in Sekunden zwischen **End_time** und **Last_commit_cdc_time** in der Sitzung. Dieser Leistungsindikator wird am Ende der Phase 7 aufgefüllt.<br /><br /> Wenn **Session_id** = 0, die letzte latenzzeitwert von einer Sitzung aufgezeichnet.|  
|**empty_scan_count**|**int**|Anzahl der aufeinander folgenden Sitzungen, die keine Change Data Capture-Transaktionen enthalten haben.|  
|**failed_sessions_count**|**int**|Anzahl der fehlgeschlagenen Sitzungen.|  
  
## <a name="remarks"></a>Hinweise  
 Die Werte in dieser dynamischen Verwaltungssicht werden immer dann zurückgesetzt, wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung zum Abfragen der **dm_cdc_log_scan_sessions** -verwaltungssicht. Weitere Informationen zu Berechtigungen für dynamische Verwaltungssichten finden Sie unter [dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zur aktuellen Sitzung zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase  
    error_count, start_lsn, current_lsn, end_lsn, tran_count  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [dm_cdc_errors &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

