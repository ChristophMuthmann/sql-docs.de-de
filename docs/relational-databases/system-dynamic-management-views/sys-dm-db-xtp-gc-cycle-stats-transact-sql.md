---
title: dm_db_xtp_gc_cycle_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_gc_cycle_stats_TSQL
- dm_db_xtp_gc_cycle_stats
- sys.dm_db_xtp_gc_cycle_stats_TSQL
- sys.dm_db_xtp_gc_cycle_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_gc_cycle_stats dynamic management view
ms.assetid: bbc9704e-158e-4d32-b693-f00dce31cd2f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cce841247a51be5580cece7e023bed3ebc7581e2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbxtpgccyclestats-transact-sql"></a>sys.dm_db_xtp_gc_cycle_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Gibt den aktuellen Status von Transaktionen aus, durch die mindestens eine Zeile gelöscht und für die ein Commit ausgeführt wurde. Der Garbage Collection-Leerlaufthread wird einmal pro Minute ausgeführt oder wenn die Anzahl der DML-Transaktionen, für die ein Commit ausgeführt wurde, seit dem letzten Zyklus der Garbage Collection einen internen Schwellenwert überschreitet. Im Zyklus der Garbage Collection werden die Transaktionen, für die ein Commit ausgeführt wurde, in eine oder mehrere Warteschlangen verschoben, die unterschiedlichen Generierungen zugeordnet sind. Transaktionen, durch die veraltete Versionen generiert wurden, werden in einer Einheit von 16 Transaktionen gruppiert, die sich wie folgt über 16 Generierungen verteilen:  
  
-   Generierung 0: Speichert alle Transaktionen, für die vor der ältesten aktiven Transaktion ein Commit ausgeführt wurde. Von diesen Transaktionen generierte Zeilenversionen stehen sofort für die Garbage Collection zur Verfügung.  
  
-   Generierungen 1-14: Speichern Transaktionen, deren Zeitstempel nach der ältesten aktiven Transaktion liegt. Die Zeilenversionen können nicht von der Garbage Collection bereinigt werden. Jede Generierung kann bis zu 16 Transaktionen enthalten. In den Generierungen können insgesamt 224 (14 * 16) Transaktionen gespeichert werden.  
  
-   Generierung 15: Enthält die übrigen Transaktionen, deren Zeitstempel nach der ältesten aktiven Transaktion liegt. Die Anzahl der Transaktionen in Generierung 15 ist genauso wie bei Generierung 0 unbegrenzt.  
  
 Bei unzureichendem Arbeitsspeicher wird der Hinweis auf die älteste aktive Transaktion vom Garbage Collection-Thread aggressiv aktualisiert, wodurch eine Garbage Collection erzwungen wird.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|cycle_id|**bigint**|Ein eindeutiger Bezeichner für den Zyklus der Garbage Collection.|  
|ticks_at_cycle_start|**bigint**|Takte, bei denen der Zyklus gestartet wurde.|  
|ticks_at_cycle_end|**bigint**|Takte, bei denen der Zyklus beendet wurde.|  
|base_generation|**bigint**|Der aktuelle Basisgenerierungswert in der Datenbank. Dieser entspricht dem Zeitstempel der ältesten aktiven Transaktion, mit dessen Hilfe Transaktionen für die Garbage Collection identifiziert werden. Die ID der ältesten aktiven Transaktion wird in Schritten von 16 aktualisiert. Beispiel: Wenn die Transaktions-IDs 124, 125, 126 … 139 lauten, beträgt der Wert 124. Wenn Sie eine weitere Transaktion, z. B. 140, hinzufügen, ist der Wert 140.|  
|xacts_copied_to_local|**bigint**|Die Anzahl der Transaktionen, die aus der Transaktionspipeline in das Generierungsarray der Datenbank kopiert wurden.|  
|xacts_in_gen_0- xacts_in_gen_15|**bigint**|Die Anzahl der Transaktionen in jeder Generierung.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung auf dem Server.  
  
## <a name="usage-scenario"></a>Verwendungsszenario  
 Im Folgenden eine Beispielausgabe. Zu sehen sind eine Teilmenge der Spalten und 27 Generierungen:  
  
```  
cycle_id   ticks_at_cycle_start ticks_at_cycle_end   base_generation  xacts_in_gen_0    xacts_in_gen_1  
  
1          123160509            123160509            1                    0                    0  
2          123176822            123176822            1                    0                    1  
3          123236826            123236826            1                    0                    1  
4          123296829            123296829            1                    0                    1  
5          123356832            123356941            129                  0                    0  
6          123357473            123357473            129                  0                    0  
7          123417486            123417486            129                  0                    0  
8          123477489            123477489            129                  0                    0  
9          123537492            123537492            129                  0                    0  
10         123597500            123597500            129                  0                    0  
11         123657504            123657504            129                  0                    0  
12         123717507            123717507            129                  0                    0  
13         123777510            123777510            129                  0                    0  
14         123837513            123837513            129                  0                    0  
15         123897516            123897516            129                  0                    0  
16         123957516            123957516            129                  0                    0  
17         124017516            124017516            129                  0                    0  
18         124077517            124077517            129                  0                    0  
19         124137517            124137517            129                  0                    0  
20         124197518            124197518            129                  0                    0  
21         124257518            124257518            129                  0                    0  
22         124317523            124317523            129                  0                    0  
23         124377526            124377526            129                  0                    0  
24         124437529            124437529            129                  0                    0  
25         124497533            124497533            129                  0                    0  
26         124557536            124557536            129                  0                    0  
27         124617539            124617539            129                  0                    0  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten für Speicheroptimierte Tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
