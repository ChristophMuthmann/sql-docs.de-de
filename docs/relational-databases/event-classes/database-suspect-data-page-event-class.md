---
title: Database Suspect Data Page-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b6882a854d3cb6ea7f4febf7d66ecf09f20e9e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="database-suspect-data-page-event-class"></a>Database Suspect Data Page-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Die Ereignisklasse **Database Suspect Data Page** zeigt an, dass der [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md)-Tabelle in [msdb](../../relational-databases/databases/msdb-database.md) eine Seite hinzugefügt wurde. Schließen Sie diese Ereignisklasse in Ablaufverfolgungen ein, von denen das Vorkommen fehlerverdächtiger Seiten überwacht wird.  
  
> [!NOTE]  
>  Dieses Ereignis wird asynchron durch das Einfügen einer entsprechenden Zeile in der **suspect_pages** -Tabelle ausgegeben. Deshalb kann es sein, dass ein Auftrag, der dieses Ereignis überwacht, den entsprechenden **suspect_pages** -Eintrag nicht sofort findet.  
  
 Wenn die Ereignisklasse **Database Suspect Data Page** in einer Ablaufverfolgung eingeschlossen ist, ist der damit verbundene Verwaltungsaufwand gering. Der Verwaltungsaufwand ist möglicherweise höher, wenn die Anzahl der fehlerverdächtigen Seiten zunimmt, wenn beispielsweise bei einem Datenträgerlaufwerk Probleme auftreten.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Datenspalten der Database Suspect Data Page-Ereignisklasse  
  
|Name der Datenspalte|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID der Datenbank, für die das fehlerverdächtige Seitenereignis ausgelöst wurde. Dieser Wert ist identisch mit dem der Spalte **database_id** der **suspect_pages** -Tabelle.|3|Ja|  
|**EventClass**|**int**|Der Typ des Ereignisses ist 213.|27|Nein|  
|**EventSequence**|**int**|Die Sequenz der Ereignisklasse im Batch.|51|Nein|  
|**SPID**|**int**|ID des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tasks, bei dem die fehlerverdächtige Seite aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Die Uhrzeit, zu der das Ereignis aufgetreten ist.|14|Ja|  
|**ObjectID**|**int**|ID der Datenbankdatei, die die fehlerverdächtige Seite enthält. Dieser Wert ist identisch mit dem der Spalte **file_id** der **suspect_pages** -Tabelle.|22|Ja|  
|**ObjectID2**|**int**|ID der in der Datei befindlichen fehlerverdächtigen Seite. Dieser Wert ist identisch mit dem der Spalte **page_id** der **suspect_pages** -Tabelle.|56|Ja|  
|**Fehler**|**int**|Typ des aufgetretenen Fehlers. Dieser Wert ist identisch mit dem **event_type** -Wert der Seite in der **suspect_pages** -Tabelle.|31|Ja|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
