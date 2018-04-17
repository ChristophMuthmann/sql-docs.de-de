---
title: dm_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb27d263081cac5975e8a68a1cf13004fb1d2759
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmfilestreamnontransactedhandles-transact-sql"></a>sys.dm_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt die derzeit geöffneten nicht transaktionalen Dateihandles an, die den FileTable-Daten zugeordnet sind.  
  
 Diese Sicht enthält eine Zeile pro geöffnetem Dateihandle. Da die Daten in dieser Sicht dem internen Livestatus des Servers entsprechen, ändern sich die Daten kontinuierlich mit dem Öffnen und Schließen der Handles. Diese Sicht enthält keine Verlaufsinformationen.  
  
 Weitere Informationen finden Sie unter [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md).  
  
|**Column**|**Typ**|**Beschreibung**|  
|----------------|--------------|---------------------|  
|database_id|int|ID der Datenbank, die dem Handle zugeordnet ist.|  
|object_id|int|Objekt-ID der FileTable, der das Handle zugeordnet ist.|  
|handle_id|int|Eindeutiger Handlekontextbezeichner. Anhand der [Sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) gespeicherten Prozedur an ein bestimmtes Handle abzubrechen.|  
|file_object_type|int|Typ des Handles. Gibt die Ebene der Hierarchie an, für die das Handle geöffnet wurde, d. h. die Datenbank oder das Element.|  
|file_object_type_desc|nvarchar(120)|“UNDEFINED",<br />“SERVER_ROOT",<br />“DATABASE_ROOT",<br />“TABLE_ROOT",<br />“TABLE_ITEM"|  
|correlation_process_id|varbinary(8)|Enthält einen eindeutigen Bezeichner für den Prozess, von dem die Anforderung stammt.|  
|correlation_thread_id|varbinary(8)|Enthält einen eindeutigen Bezeichner für den Thread, von dem die Anforderung stammt.|  
|file_context|varbinary(8)|Zeiger auf das von diesem Handle verwendete Dateiobjekt.|  
|state|int|Der aktuelle Status des Handles. Der Status kann aktiv, geschlossen oder abgebrochen sein.|  
|state_desc|nvarchar(120)|“ACTIVE",<br />“CLOSED",<br />“KILLED"|  
|current_workitem_type|int|Der aktuelle Status für die Verarbeitung dieses Handles.|  
|current_workitem_type_desc|nvarchar(120)|“NoSetWorkItemType",<br />“FFtPreCreateWorkitem",<br />“FFtGetPhysicalFileNameWorkitem",<br />“FFtPostCreateWorkitem",<br />“FFtPreCleanupWorkitem",<br />“FFtPostCleanupWorkitem",<br />“FFtPreCloseWorkitem",<br />“FFtQueryDirectoryWorkItem",<br />“FFtQueryInfoWorkItem",<br />“FFtQueryVolumeInfoWorkItem",<br />“FFtSetInfoWorkitem",<br />“FFtWriteCompletionWorkitem"|  
|fcb_id|bigint|FileTable-Dateikontrollblock-ID.|  
|item_id|varbinary(892)|Die Element-ID für eine Datei oder ein Verzeichnis. Ist möglicherweise NULL für Stammhandles des Servers.|  
|is_directory|bit|Dies ist ein Verzeichnis.|  
|item_name|nvarchar(512)|Name des Elements.|  
|opened_file_name|nvarchar(512)|Zu öffnender Pfad der ursprünglichen Anforderung.|  
|database_directory_name|nvarchar(512)|Teil des opened_file_name-Elements, das den Datenbankverzeichnisnamen darstellt.|  
|table_directory_name|nvarchar(512)|Teil des opened_file_name-Elements, das den Tabellenverzeichnisnamen darstellt.|  
|remaining_file_name|nvarchar(512)|Teil des opened_file_name-Elements, das den Namen des verbleibenden Verzeichnisses darstellt.|  
|open_time|datetime|Zeitpunkt, zu dem das Handle geöffnet wurde.|  
|flags|int|ShareFlagsUpdatedToFcb = 0x1,<br />DeleteOnClose = 0x2,<br />NewFile = 0x4,<br />PostCreateDoneForNewFile = 0x8,<br />StreamFileOverwritten = 0x10,<br />RequestCancelled = 0x20,<br />NewFileCreationRolledBack = 0x40|  
|login_id|int|ID des Prinzipals, der das Handle geöffnet hat.|  
|login_name|nvarchar(512)|Name des Prinzipals, der das Handle geöffnet hat.|  
|login_sid|varbinary(85)|SID des Prinzipals, der das Handle geöffnet hat.|  
|read_access|bit|Geöffnet für Lesezugriff.|  
|write_access|bit|Geöffnet für Schreibzugriff.|  
|delete_access|bit|Geöffnet für Löschzugriff.|  
|share_read|bit|Geöffnet mit share_read-Berechtigung.|  
|share_write|bit|Geöffnet mit share_write-Berechtigung.|  
|share_delete|bit|Geöffnet mit share_delete-Berechtigung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
