---
title: Sys. server_file_audits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_file_audits_TSQL
- sys.server_file_audits_TSQL
- sys.server_file_audits
- server_file_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_file_audits catalog view
ms.assetid: 553288a0-be57-4d79-ae53-b7cbd065e127
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 62ea18b6a942c80a70a25f749ffc6bce1c10a1c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysserverfileaudits-transact-sql"></a>sys.server_file_audits (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält erweiterte Informationen über den dateiüberwachungstyp in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Überwachung auf einer Serverinstanz. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|audit_id|**int**|Die ID der Überwachung.|  
|name|**sysname**|Der Name der Überwachung.|  
|audit_guid|**uniqueidentifier**|GUID der Überwachung.|  
|create_date|**datetime**|Das UTC-Datum, an dem die Dateiüberwachung erstellt wurde.|  
|modify_date|**datatime**|Das UTC-Datum, an dem die Dateiüberwachung zuletzt geändert wurde.|  
|principal_id|**int**|Die ID des Besitzers der Überwachung, wie sie auf dem Server registriert wurde.|  
|Typ|**char(2)**|Überwachungstyp:<br /><br /> 0 = NT-Sicherheitsereignisprotokoll<br /><br /> 1 = NT-Anwendungsereignisprotokoll<br /><br /> 2 = Datei auf Dateisystem|  
|type_desc|**nvarchar(60)**|Beschreibung des Überwachungstyps.|  
|on_failure|**tinyint**|Bei Fehlerbedingung:<br /><br /> 0 = Weiter<br /><br /> 1 = Serverinstanz herunterfahren<br /><br /> 2 = Fehler bei Vorgang|  
|on_failure_desc|**nvarchar(60)**|Bei einem Fehler schreiben Sie folgendermaßen einen Aktionseintrag:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL OPERATION|  
|is_state_enabled|**tinyint**|0 = Deaktiviert<br /><br /> 1 = Aktiviert|  
|queue_delay|**int**|Vorgeschlagene maximale Wartezeit in Millisekunden, bevor auf den Datenträger geschrieben wird. Wenn 0, garantiert die Überwachung einen Schreibvorgang, bevor das Ereignis fortgesetzt werden kann.|  
|predicate|**nvarchar(8000)**|Prädikatausdruck, der auf das Ereignis angewendet wird.|  
|max_file_size|**bigint**|Maximale Größe der Überwachungsdatei in MB:<br /><br /> 0 = Unbegrenzt/Nicht anwendbar auf den ausgewählten Überwachungstyp.|  
|max_rollover_files|**int**|Maximale Anzahl von Dateien zur Verwendung mit der Rolloveroption.|  
|max_files|**int**|Maximale Anzahl von Dateien zur Verwendung ohne die Rolloveroption.|  
|reserved_disk_space|**int**|Pro Datei zu reservierender Speicherplatz.|  
|log_file_path|**nvarchar(260)**|Pfad zum Speicherort der Überwachung. Dateipfad für Dateiüberwachung, Anwendungsprotokollpfad für Anwendungsprotokollüberwachung.|  
|log_file_name|**nvarchar(260)**|Basisname für die in CREATE AUDIT DDL angegebene Protokolldatei. Eine inkrementelle Zahl wird als Suffix an den Protokolldateinamen erstellt die Base_log_name-Datei hinzugefügt.|  
  
## <a name="permissions"></a>Berechtigungen  
 Prinzipale mit den **ALTER ANY SERVER AUDIT** oder **VIEW ANY DEFINITION** -Berechtigung haben Zugriff auf diese Katalogsicht. Darüber hinaus dem Prinzipal nicht verweigert werden muss **VIEW ANY DEFINITION** Berechtigung.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [Sys. server_file_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
