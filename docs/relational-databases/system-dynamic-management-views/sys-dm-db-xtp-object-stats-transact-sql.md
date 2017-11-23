---
title: Sys.dm_db_xtp_object_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_object_stats_TSQL
- sys.dm_db_xtp_object_stats
- dm_db_xtp_object_stats
- sys.dm_db_xtp_object_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_xtp_object_stats dynamic management view
ms.assetid: 07300b59-3cab-4d3e-8138-5ea8f584f88f
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b07eb152c42c2f9c991d99ff6e3256b62d1cef8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbxtpobjectstats-transact-sql"></a>sys.dm_db_xtp_object_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Meldet die Anzahl der Zeilen von Operationen auf allen betroffenen der [!INCLUDE[hek_2](../../includes/hek-2-md.md)] Objekte seit dem letzten Neustart. Die Statistiken werden aktualisiert, wenn der Vorgang ausgeführt wird, und zwar unabhängig davon, ob für die Transaktion ein Commit oder Rollback ausgeführt wurde.  
  
 Mithilfe von sys.dm_db_xtp_object_stats können Sie ermitteln, welche speicheroptimierten Tabellen am häufigsten geändert werden. Sie können selten oder nicht verwendete Tabellenindizes entfernen, da jeder Index die Leistung beeinflusst. Bei Verwendung von Hashindizes sollte die Bucketanzahl regelmäßig neu ausgewertet werden. Weitere Informationen finden Sie unter [Determining the Correct Bucket Count for Hash Indexes](http://msdn.microsoft.com/library/6d1ac280-87db-4bd8-ad43-54353647d8b5).  
  
 Mithilfe von sys.dm_db_xtp_object_stats können Sie ermitteln, welche speicheroptimierten Tabellen Write-Write-Konflikte verursachen, die möglicherweise die Anwendungsleistung beeinträchtigen. Wenn Sie beispielsweise Wiederholungslogik für Transaktionen implementiert haben, muss ein und dieselbe Anweisung u. U. mehrfach ausgeführt werden. Außerdem können Sie anhand dieser Informationen die Tabellen (und folglich die Geschäftslogik) identifizieren, die eine Behandlung von Write-Write-Fehlern erfordern.  
  
 Diese Sicht enthält eine Zeile für jede speicheroptimierte Tabelle in der Datenbank.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|Die ID des Objekts.|  
|row_insert_attempts|**bigint**|Die Anzahl der Zeilen, die seit dem letzten Neustart der Datenbank von Transaktionen, für die ein Commit oder Abbruch ausgeführt wurde, in die Tabelle eingefügt wurden.|  
|row_update_attempts|**bigint**|Die Anzahl der Zeilen, die seit dem letzten Neustart der Datenbank von Transaktionen, für die ein Commit oder Abbruch ausgeführt wurde, in der Tabelle aktualisiert wurden.|  
|row_delete_attempts|**bigint**|Die Anzahl der Zeilen, die seit dem letzten Neustart der Datenbank von Transaktionen, für die ein Commit oder Abbruch ausgeführt wurde, aus der Tabelle gelöscht wurden.|  
|write_conflicts|**bigint**|Die Anzahl der Schreibkonflikte, die seit dem letzten Neustart der Datenbank aufgetreten sind.|  
|unique_constraint_violations|**bigint**|Die Anzahl der Verletzungen von UNIQUE-Einschränkungen, die seit dem letzten Neustart der Datenbank aufgetreten sind.|  
|object_address|**varbinary(8)**|Nur interne Verwendung.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung für die aktuelle Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten für Speicheroptimierte Tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
