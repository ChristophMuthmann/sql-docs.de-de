---
title: Sys. remote_data_archive_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29d6916024358efb9e806a5f8d1eeaf6a3715d89
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Stretch-Datenbank-Katalogsichten - Sys. remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Remotetabelle, die Daten aus einer lokalen mit aktivierter Funktion Stretch-Tabelle speichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die Objekt-ID der lokalen Tabelle für Stretch aktiviert werden soll.|  
|**remote_database_id**|**int**|Der automatisch generierten lokale Bezeichner der Remotedatenbank.|  
|**remote_table_name**|**sysname**|Der Name der Tabelle in der Remotedatenbank, die die Stretch-aktivierte lokale Tabelle entspricht.|  
|**filter_predicate**|**nvarchar(max)**|Das Filterprädikat, sofern vorhanden, identifiziert, die Zeilen in der Tabelle migriert werden. Falls der Wert NULL ist, ist die gesamte Tabelle für die Migration geeignet.<br /><br /> Weitere Informationen finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) und [auswählen zu migrierender mithilfe der Filter-Prädikat Zeilen](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|Die Richtung, in der Daten gerade migriert wird. Die verfügbaren Werte sind die folgenden.<br/>1 (ausgehend)<br/>2 (eingehend)|  
|**migration_direction_desc**|**nvarchar(60)**|Die Beschreibung der die Richtung, in der Daten gerade migriert wird. Die verfügbaren Werte sind die folgenden.<br/>ausgehend (1)<br/>eingehende (2)|  
|**is_migration_paused**|**bit**|Gibt an, ob die Migration angehalten wird.|  
|**is_reconciled**|**bit**| Gibt an, ob die Remotetabelle und SQL Server-Tabelle synchronisiert sind.<br/><br/>Wenn der Wert der **Is_reconciled** ist 1 (True), die Remotetabelle und SQL Server-Tabelle synchronisiert werden und können Sie Abfragen, die Remotedaten enthalten, ausführen.<br/><br/>Wenn der Wert der **Is_reconciled** ist 0 (False), die Remotetabelle und SQL Server-Tabelle sind nicht synchronisiert. Haben kürzlich migrierte Zeilen erneut migriert werden. Dies tritt auf, wenn Sie die Azure-Remotedatenbank wiederherstellen oder wenn Sie Zeilen manuell aus der Remotetabelle löschen. Bis Sie die Tabellen abstimmen möchten, können nicht Sie Abfragen ausführen, die die Remotedaten enthalten. Führen Sie die Tabellen ausgleichen möchten, [sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Siehe auch  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

