---
title: Stretch-Datenbank, die erweiterte gespeicherte Prozeduren (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68ef74d212ac3ad0e4ec7da5866390df8c8bce7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch-Datenbank erweiterte gespeicherte Prozeduren (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Dieser Abschnitt beschreibt die erweiterten gespeicherten Prozeduren, die mit Stretch-Datenbank verknüpft sind.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
[Sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) entfernt die authentifizierte Verbindung zwischen einer lokalen Stretch-aktivierte Datenbank und der Azure-Remotedatenbank.

[sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) Ruft die Anzahl von Stunden für migrierte Daten, die von SQL Server beibehalten in eine Stagingtabelle für Hilfe eine vollständige Wiederherstellung der Azure-Remotedatenbank, stellen Sie sicher, wenn eine Wiederherstellung erforderlich ist.
  
 [Sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) die authentifizierte Verbindung zwischen einer lokalen Datenbank für Stretch aktiviert und die remote-Datenbank wiederhergestellt.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Gleicht die Batch-ID, die in der Stretch-aktivierten SQL Server-Tabelle für die meisten zuletzt migrierten Daten gespeichert werden, mit der Batch-ID, die in der remote-Azure-Tabelle gespeichert. 
 
[sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) gleicht die Spalten in der Azure-Remotetabelle den Spalten in der Stretch-aktivierten SQL Server-Tabelle.
 
 [Sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) Warteschlangen eine Schemaaufgabe um Indizes für die Remotetabelle abzustimmen.
 
 [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) gibt an, ob Abfragen an der aktuellen Stretch-aktivierte Datenbank und zugehörigen Tabellen sowohl lokale als auch Daten (Standard) oder nur lokale Daten zurückgeben.
 
 [Sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) wird die Anzahl von Stunden für migrierte Daten, die von SQL Server beibehalten in eine Stagingtabelle für Hilfe eine vollständige Wiederherstellung der Azure-Remotedatenbank, stellen Sie sicher, wenn eine Wiederherstellung erforderlich ist.
 
 [Sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) testet die Verbindung von SQL Server mit der Azure-Remoteserver und meldet Probleme, die Migration von Daten verhindern können.
 
## <a name="see-also"></a>Siehe auch  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
