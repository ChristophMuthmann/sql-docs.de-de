---
title: Verwalten und Problembehandlung von Stretch Database | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/27/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Stretch Database, managing
- Stretch Database, troubleshooting
- managing Stretch Database
- troubleshooting Stretch Database
ms.assetid: 6334db3e-9297-44df-8d53-211187a95520
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fbf7811bb7ccbd1ba7867797ab326642c5d7587e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="manage-and-troubleshoot-stretch-database"></a>Verwalten und Problembehandlung von Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Verwenden Sie die in diesem Artikel beschriebenen Tools und Methoden, um Stretch Database zu verwalten und Probleme zu behandeln.  
## <a name="manage-local-data"></a>Verwalten von lokalen Daten  
  
###  <a name="LocalInfo">
            </a> Abrufen von Informationen zu lokalen Datenbanken und Tabellen, die für Stretch Database aktiviert sind  
 Öffnen Sie die Katalogsichten **sys.databases** und **sys.tables** , um Informationen über SQL Server-Datenbanken und -Tabellen zu finden, die für Stretch aktiviert sind. Weitere Informationen finden Sie unter [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) und [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md).  
 
 Führen Sie die folgende Anweisung aus, um zu ermitteln, wie viel Speicherplatz eine Stretch-aktivierte Tabelle in SQL Server verwendet.
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'LOCAL_ONLY';
GO
 ```
   
## <a name="manage-data-migration"></a>Verwalten der Datenmigration  
  
### <a name="check-the-filter-function-applied-to-a-table"></a>Überprüfen der auf eine Tabelle angewendeten Filterfunktion  
 Öffnen Sie die Katalogsicht **sys.remote_data_archive_tables** , und überprüfen Sie den Wert der **filter_predicate** -Spalte, um die Funktion zu identifizieren, die von Stretch Database verwendet wird, um die zu migrierenden Zeilen auszuwählen. Falls der Wert NULL ist, ist die gesamte Tabelle für die Migration geeignet. Weitere Informationen finden Sie unter [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md) und [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
###  <a name="Migration"></a> Überprüfen des Status der Datenmigration  
 Wählen Sie, zum Überwachen der Datenmigration in der Stretch Database-Überwachung **Aufgaben | Stretch | Überwachen** für eine Datenbank in SQL Server Management Studio aus. Weitere Informationen finden Sie unter [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
 Oder öffnen Sie die dynamische Verwaltungssicht **sys.dm_db_rda_migration_status** , um anzuzeigen, wie viele Batches und Datenzeilen migriert wurden.  
  
###  <a name="Firewall"></a> Problembehandlung der Datenmigration  
 Weitere Empfehlungen zur Problembehandlung finden Sie unter [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
## <a name="manage-remote-data"></a>Verwalten von Remotedaten  
  
###  <a name="RemoteInfo">
            </a> Abrufen von Informationen zu Remotedatenbanken und Tabellen, die von Stretch Database verwendet werden  
 Öffnen Sie die Katalogsichten **sys.remote_data_archive_databases** und **sys.remote_data_archive_tables** , um Informationen über die Remotedatenbanken und Tabellen zu finden, in denen migrierte Daten gespeichert sind. Weitere Informationen finden Sie unter [sys.remote_data_archive_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md) und [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md).  
 
Führen Sie die folgende Anweisung aus, um zu ermitteln, wie viel Speicherplatz eine Stretch-aktivierte Tabelle in Azure verwendet.
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'REMOTE_ONLY';
GO
 ```

### <a name="delete-migrated-data"></a>Löschen von migrierten Daten  
Wenn Sie bereits zu Azure migrierte Daten löschen möchten, befolgen Sie die in [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)beschriebenen Schritte.  
  
## <a name="manage-table-schema"></a>Verwalten von Tabellenschemas

### <a name="dont-change-the-schema-of-the-remote-table"></a>Verändern Sie das Schema der Remotetabelle nicht  
 Ändern Sie das Schema einer Remote-Azure-Tabelle nicht, wenn diese mit einer SQL Server-Tabelle verknüpft ist, die für Stretch Database konfiguriert ist. Ändern Sie insbesondere nicht den Namen oder den Datentyp einer Spalte. Die Stretch Database-Funktion trifft diverse Annahmen über das Schema der Remotetabelle in Bezug auf das Schema der SQL Server-Tabelle. Falls Sie das Remoteschema ändern, funktioniert Stretch Database nicht mehr für die geänderte Tabelle.  

### <a name="reconcile-table-columns"></a>Abstimmen von Tabellenspalten  
Wenn Sie Spalten aus der Remotetabelle versehentlich gelöscht haben, führen Sie **sp_rda_reconcile_columns** aus, um Spalten zur Remotetabelle hinzuzufügen, die in der Stretch-aktivierten SQL Server-Tabelle, aber nicht in der Remotetabelle vorhanden sind. Weitere Informationen finden Sie unter [sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md).  
  
  > [!IMPORTANT]
  > Wenn **sp_rda_reconcile_columns** Spalten neu erstellt, die Sie versehentlich aus der Remotetabelle gelöscht haben, dann werden nicht die zuvor in den gelöschten Spalten enthaltenen Daten wiederhergestellt.
  
**sp_rda_reconcile_columns** löscht keine Spalten aus der Remotetabelle, die in der Remotetabelle, aber nicht in der Stretch-aktivierten SQL Server-Tabelle vorhanden sind. Wenn Spalten in der Azure-Remotetabelle enthalten sind, die in der Stretch-aktivierten SQL Server-Tabelle nicht mehr vorhanden sind, dann verhindern diese zusätzlichen Spalten nicht, dass Stretch Database ordnungsgemäß arbeitet. Sie können die zusätzlichen Spalten optional manuell entfernen.  
 
## <a name="manage-performance-and-costs"></a>Verwalten von Leistung und Kosten  
  
### <a name="troubleshoot-query-performance"></a>Problembehandlung der Abfrageleistung  
  Bei Abfragen, die Stretch-aktivierte Tabellen enthalten, wird erwartet, dass sie langsamer ausgeführt werden, als zum Zeitpunkt bevor die Tabellen für Stretch aktiviert wurden. Falls die Abfrageleistung erheblich beeinträchtigt wird, überprüfen Sie die folgenden möglichen Probleme.  
  
-   Befindet sich Ihr Azure-Server in einer anderen geografischen Region als Ihr SQL Server? Konfigurieren Sie Ihren Azure-Server dahingehend, dass er sich in der gleichen geografischen Region wie Ihr SQL Server befindet, um die Netzwerklatenz zu reduzieren.  
  
-   Möglicherweise haben sich Ihre Netzwerkbedingungen verschlechtert. Wenden Sie sich an Ihren Netzwerkadministrator, um Informationen über aktuelle Probleme oder Ausfälle zu erhalten.  
  
### <a name="increase-azure-performance-level-for-resource-intensive-operations-such-as-indexing"></a>Erhöhen der Azure-Leistungsstufe für ressourcenintensive Vorgänge wie z.B. Indizierung  
 Wenn Sie einen Index für eine große Tabelle, die für Stretch Database konfiguriert ist, erstellen, neuerstellen, oder neuorganisieren und Sie während dieses Zeitraums zahlreiche Abfragen für die migrierten Daten in Azure erwarten, dann ziehen Sie in Betracht, die Leistungsstufe der entsprechenden Azure-Remotedatenbank für die Dauer des Vorganges zu erhöhen. Weitere Informationen zu Leistungsstufen und Preisen finden Sie unter [SQL Server Stretch Database – Preise](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="you-cant-pause-the-sql-server-stretch-database-service-on-azure"></a>Sie können den SQL Server Stretch Database-Dienst in Azure nicht anhalten.  
 Stellen Sie sicher, dass Sie die entsprechenden Leistungs- und Preisstufen auswählen. Wenn Sie die Leistungsstufe für einen ressourcenintensiver Vorgang vorübergehend erhöhen, stellen Sie die vorherige Stufe nach Abschluss des Vorgangs wieder her. Weitere Informationen zu Leistungsstufen und Preisen finden Sie unter [SQL Server Stretch Database – Preise](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
   
 ## <a name="change-the-scope-of-queries"></a>Ändern des Bereichs von Abfragen  
 Abfragen für Stretch-aktivierte Tabellen geben standardmäßig sowohl lokale als auch Remotedaten zurück. Sie können den Bereich von Abfragen für alle Abfragen von allen Benutzern oder nur für eine einzelne Abfrage von einem Administrator ändern.  
   
 ### <a name="change-the-scope-of-queries-for-all-queries-by-all-users"></a>Ändern des Bereichs von Abfragen für alle Abfragen von allen Benutzern  
 Um den Bereich aller Abfragen von allen Benutzern zu ändern, führen Sie die gespeicherte Prozedur **sys.sp_rda_set_query_mode**aus. Sie können den Bereich eingrenzen, sodass nur lokale Daten abgefragt werden, und Sie können alle Abfragen deaktivieren oder die Standardeinstellung wiederherstellen. Weitere Informationen finden Sie unter [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md).  
   
 ### <a name="queryHints"></a>Ändern des Bereichs von Abfragen für eine einzelne Abfrage von einem Administrator  
 Zum Ändern des Bereichs einer einzelnen Abfrage von einem Mitglied der Rolle „db_owner“ fügen Sie den Abfragehinweis ***WITH ( REMOTE_DATA_ARCHIVE_OVERRIDE =* value)** zur SELECT-Anweisung hinzu. Der REMOTE_DATA_ARCHIVE_OVERRIDE-Abfragehinweis kann die folgenden Werte enthalten.  
 -   **LOCAL_ONLY**. Es werden nur lokale Daten abgefragt.  
   
 -   **REMOTE_ONLY**. Es werden nur Remotedaten abgefragt.  
   
 -   **STAGE_ONLY**. Es werden nur die Daten in der Tabelle abgefragt, für die Stretch Database für die Migration geeignete Zeilen bereitstellt und migrierte Zeilen für den angegebenen Zeitraum nach der Migration beibehält. Dieser Abfragehinweis ist die einzige Möglichkeit zum Abfragen der Stagingtabelle.  
  
Die folgende Abfrage gibt z. B. nur lokale Ergebnisse zurück.  
  
 ```sql  
USE <Stretch-enabled database name>;
GO
SELECT * FROM <Stretch_enabled table name> WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = LOCAL_ONLY) WHERE ... ;
GO
```  
   
 ## <a name="adminHints"></a>Durchführen administrativer Aktualisierungs- und Löschvorgänge  
 Standardmäßig können Sie Zeilen, die für die Migration geeignet sind oder bereits migriert wurden, in einer Stretch-aktivierten Tabelle nicht aktualisieren oder löschen. Wenn Sie ein Problem beheben müssen, kann ein Mitglied der Rolle „db_owner“ einen UPDATE- oder DELETE-Vorgang durch Hinzufügen des Abfragehinweises ***WITH ( REMOTE_DATA_ARCHIVE_OVERRIDE =* value)** zur Anweisung ausführen. Der REMOTE_DATA_ARCHIVE_OVERRIDE-Abfragehinweis kann die folgenden Werte enthalten.  
 -   **LOCAL_ONLY**. Aktualisieren oder löschen Sie nur lokale Daten.  
   
 -   **REMOTE_ONLY**. Aktualisieren oder löschen Sie nur Remotedaten.  
   
 -   **STAGE_ONLY**. Aktualisieren oder löschen Sie nur die Daten in der Tabelle, für die Stretch Database für die Migration geeignete Zeilen bereitstellt und migrierte Zeilen für den angegebenen Zeitraum nach der Migration beibehält.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)   
[Sichern von Stretch-aktivierten Datenbanken (Stretch Database)](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
[Wiederherstellen von Stretch-aktivierten Datenbanken (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
  
