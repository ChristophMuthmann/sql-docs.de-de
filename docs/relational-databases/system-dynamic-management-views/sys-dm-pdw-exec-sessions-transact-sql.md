---
title: Sys.dm_pdw_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbec94d3778bf9b898f9b0f789a644d39829ae5a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>Sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Sitzungen auf dem Gerät zurzeit oder zuletzt geöffnet. Sie enthält eine Zeile pro Sitzung.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|Die Id der aktuellen Abfrage oder der letzten Abfrage ausführen (wenn die Sitzung beendet wird, und zum Zeitpunkt der Beendigung die Abfrage ausgeführt wurde). Der Schlüssel für diese Ansicht.|Für alle Sitzungen im System eindeutig.|  
|status|**nvarchar(10)**|Für die aktuelle Sitzung identifiziert, ob die Sitzung derzeit aktiv oder inaktiv ist. Für die letzten Sitzungen die Sitzungskonfiguration Status anzeigen kann geschlossen oder abgebrochen wird (wenn die Sitzung zwangsweise geschlossen wurde).|"LEERLAUF", "ACTIVE", "GESCHLOSSEN", BEENDET""|  
|request_id|**nvarchar(32)**|Die Id der aktuellen Abfrage oder des letzten Abfrage, die ausgeführt werden soll.|Für alle Anforderungen im System eindeutig. NULL, wenn keine ausgeführt wurde.|  
|security_id|**varbinary (85)**|Sicherheits-ID des Prinzipals, der die Sitzung ausführt.||  
|login_name|**vom Datentyp nvarchar(128)**|Der Anmeldename, der der Prinzipal, der die Sitzung ausgeführt werden soll.|Eine beliebige Zeichenfolge, die die Benutzer-Benennungskonventionen entsprechen.|  
|login_time|**datetime**|Datum und Uhrzeit, an dem der Benutzer angemeldet, und dieser Sitzung erstellt wurde.|Gültige **"DateTime"** vor der aktuellen Uhrzeit.|  
|query_count|**int**|Erfasst die Anzahl der Abfragen/BeschreibungDiese Sitzung wurde seit der Erstellung ausgeführt werden.|Größer als oder gleich 0.|  
|is_transactional|**bit**|Erfasst, ob eine Sitzung derzeit innerhalb einer Transaktion oder nicht.|für automatische Commits 0, 1 für transaktional.|  
|"client_id"|**nvarchar(255)**|Zeichnet Clientinformationen für die Sitzung.|Jede gültige Zeichenfolge.|  
|app_name|**nvarchar(255)**|Zeichnet Namen Anwendungsinformationen, die im Rahmen des Verbindungsprozesses optional festlegen.|Jede gültige Zeichenfolge.|  
|sql_spid|**int**|Die Id-Nummer der SPID. Verwenden der `session_id` dieser Sitzung. Verwenden der `sql_spid` Spalte zum Hinzufügen zur **sys.dm_pdw_nodes_exec_sessions**.<br /><br /> **\*\*Warnung \* \***  enthält diese Spalte-geschlossene SPIDs.||  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie im Abschnitt "maximale Systemwerte anzeigen" in der [Mindest- und Höchstwerte (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) Thema.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW SERVER STATE` Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
