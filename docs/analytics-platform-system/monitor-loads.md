---
title: "Monitor lädt für Parallel Datawarehouse"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Sie können überwachen, aktive und aktuelle [Dwloader](dwloader.md) mithilfe der Verwaltungskonsole Analytics Platform System (APS) oder die Parallel Data Warehouse (PDW)-Systemsichten lädt."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c0c55c16-00bc-4676-8970-a8e10b3e9408
caps.latest.revision: "6"
ms.openlocfilehash: 988c34b248b0058941f53575a79e4f3b6acb4de0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="monitor-loads"></a>Überwachen der Auslastung
Sie können überwachen, aktive und aktuelle [Dwloader](dwloader.md) lädt mithilfe der Verwaltungskonsole Analytics Platform System (APS) oder Parallel Data Warehouse (PDW) [Systemsichten](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/). 
  
> [!TIP]  
> Einige lädt werden mithilfe von INSERT-Anweisungen oder Business Intelligence-Tools, die SQL-Anweisungen verwenden, um die Replikatladevorgang initiiert. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Voraussetzungen  
Unabhängig von der Methode, die zum Überwachen der Auslastung verwendet wird muss die Anmeldung über die Berechtigung zum Zugriff auf die zugrunde liegenden Datenquellen verfügen. 

<!-- MISSING LINKS
For the permissions to grant, see “Use All of the Admin Console” in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>Überwachen der Auslastung  
In den folgenden Abschnitten wird beschrieben, wie Lasten zu überwachen.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>Lädt mithilfe der Verwaltungskonsole überwachen  
  
1.  Melden Sie sich bei der Verwaltungskonsole. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  Klicken Sie im oberen Menü auf **lädt**. Sie sehen, sortierbar Aufstellung aller letzten und aktiver Ladevorgänge sowie zusätzliche Informationen, z. B., ob der Auslastungstest abgeschlossen ist oder noch aktiv ist. Klicken Sie auf die Spaltenüberschriften, um die Zeilen zu sortieren.  
  
3.  Um zusätzliche Details für eine bestimmte Auslastung anzuzeigen, klicken Sie auf die Last **ID** in der linken Spalte. In der Detailansicht können Sie zu den einzelnen Schritten des Ladevorgangs Status anzuzeigen.  
  
Diese Systemsichten Informationen finden Sie die Metadaten über die Last, die in der Verwaltungskonsole angezeigt wird:  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx.md)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>Lädt mithilfe von Systemsichten überwachen  
Führen Sie zum Überwachen von aktiven und aktuell lädt mithilfe von SQL Server PDW-Ansichten die folgenden Schritte aus. Jede Systemsicht, die verwendet wird finden Sie in der Dokumentation für diese Sicht Informationen für die Spalten und die möglichen Werte, die von der Sicht zurückgegeben.  
  
1.  Suchen der `request_id` für das Laden in das [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) Ansicht mit einer Suche nach dem Ladeprogramm Befehlszeile in der `command` Spalte für diese Ansicht.  
  
    Beispielsweise der folgende Befehl gibt, die Befehlstext und den aktuellen Status sowie die `request_id`.  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  Verwenden der `request_id` zum Abrufen von zusätzlichen Informationen für das Laden mithilfe der [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) , und [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) Ansichten. Z. B. die folgende Abfrage gibt die `run_id` und Informationen über die starten, beenden und Dauer, wie oft die Last sowie Fehler und Informationen über die Anzahl der verarbeiteten Zeilen:  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id=’12738’;  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
