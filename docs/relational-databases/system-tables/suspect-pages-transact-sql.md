---
title: Suspect_pages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs: TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3dba370508c90a07cc66c4f4ef97c8d3d21d82c7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="suspectpages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile pro Seite, die mit geringfügiger Fehler 823 oder 824 Fehler fehlgeschlagen. Von den in dieser Tabelle aufgelisteten Seiten wird angenommen, dass sie fehlerhaft sind. Dies trifft jedoch möglicherweise nicht zu. Wenn eine fehlerverdächtige Seite repariert wird, wird ihr Status in der **event_type** -Spalte aktualisiert.  
  
 Die folgende Tabelle kann maximal 1.000 Zeilen umfassen und wird in der Datenbank **msdb** gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, auf die sich diese Seite bezieht.|  
|**FILE_ID**|**int**|ID der Datei in der Datenbank.|  
|**Page_ID**|**bigint**|ID der fehlerverdächtigen Seite. Jede Seite hat eine Seiten-ID, bei der es sich um einen 32-Bit-Wert handelt, die den Speicherort der Seite in der Datenbank identifiziert. **page_id** ist der Offset in die Datendatei der 8-KB-Seite. Jede Seiten-ID ist innerhalb einer Datei eindeutig.|  
|**event_type**|**int**|Einer der folgenden Fehlertypen:<br /><br /> 1 = Ein Fehler vom Typ 823, der eine fehlerverdächtige Seite verursacht (z. B. ein Datenträgerfehler) oder ein Fehler vom Typ 824, der außer einer fehlerhaften Prüfsumme oder einer zerrissenen Seite z. B. eine fehlerhafte Seiten-ID anzeigt.<br /><br /> 2 = Fehlerhafte Prüfsumme<br /><br /> 3 = Zerrissene Seite<br /><br /> 4 = Wiederhergestellt (die Seite wurde wiederhergestellt, nachdem sie als ungültig gekennzeichnet wurde)<br /><br /> 5 = Repariert (DBCC hat die Seite repariert)<br /><br /> 7 = Zuordnung durch DBCC aufgehoben|  
|**error_count**|**int**|Häufigkeit, mit der ein Fehler aufgetreten ist.|  
|**last_update_date**|**datetime**|Datums- und Zeitstempel des letzten Updates.|  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder mit Zugriff auf **msdb** kann die Daten in der Tabelle **suspect_pages** lesen. Jeder mit UPDATE-Berechtigung für die suspect_pages-Tabelle kann ihre Datensätze aktualisieren. Mitglieder der festen Datenbankrolle **db_owner** auf **msdb** oder der festen Serverrolle **sysadmin** können Datensätze einfügen, aktualisieren und löschen.  
  
## <a name="see-also"></a>Siehe auch  
 [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Database Suspect Data Page-Ereignisklasse](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
