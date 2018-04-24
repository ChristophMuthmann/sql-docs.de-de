---
title: Überwachen von aktiven Abfragen - Parallel Data Warehouse | Microsoft Docs
description: Verwenden Sie die-Verwaltungskonsole als auch Parallel Data Warehouse-Systemsichten auf aktive Abfragen auf Analytics Platform System überwachen.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 057e5448b68ea7a7f8f23bc57d1a3b0308b300d2
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Überwachen von aktiven Abfragen - Parallel Data Warehouse
In diesem Artikel wird gezeigt, wie die-Verwaltungskonsole und die SQL Server PDW-Systemsichten zu verwenden, um aktive Abfragen zu überwachen. Finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole](monitor-the-appliance-by-using-the-admin-console.md) und [Systemsichten](tsql-system-views.md) Informationen zu diesen Tools.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Unabhängig von der Methode, die zum Überwachen von aktiven Abfragen verwendet wird, muss die Anmeldung in in "Verwenden alle von der Verwaltungskonsole" beschriebenen Berechtigungen haben [Erteilen von Berechtigungen zum Verwenden der Verwaltungskonsole](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="PermsAdminConsole"></a>Monitor aktive Abfragen  
Die-Verwaltungskonsole und die SQL Server PDW-Systemsichten können verwendet werden, um aktive Abfragen zu überwachen. Führen Sie die folgenden Anweisungen aus.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Auf aktive Abfragen zu überwachen, indem Sie mithilfe der Verwaltungskonsole  
  
1.  Melden Sie sich bei der Verwaltungskonsole. Finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole](monitor-the-appliance-by-using-the-admin-console.md) Anweisungen.  
  
2.  Klicken Sie im oberen Menü auf **Abfragen**. Sehen Sie eine Tabelle mit grundlegenden Informationen zu den neuesten Abfragen auf dem Gerät, einschließlich der Anmeldename, der die Abfrage, die Start- und Endzeiten für die Abfrage und den aktuellen Status der Abfrage übermittelt.  
  
3.  Um den Abfragebefehl, zeigen Sie den Mauszeiger über den Abfrage-ID in der linken Spalte für diese Zeile anzuzeigen.  
  
    Um ausführlichere Informationen für eine bestimmte Abfrage angezeigt wird, klicken Sie auf die Abfrage-ID. Sehen Sie Informationen, einschließlich der vollständigen Abfrage und den Abfrageplan mit Statusinformationen für jeden Schritt in der Ausführung der Abfrage ein. Wenn keine Fehler zurückgegeben wurden, sehen Sie auch ausführliche Informationen zu den Fehlern. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Zum Überwachen von aktiven Abfragen mithilfe von Systemsichten  
Ist die primäre Systemsicht verwendet, um Abfragen zu überwachen [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Verwenden Sie diese Systemsicht finden die `request_id` für eine aktive oder aktuelle Abfrage, die basierend auf den Text der Abfrage.  
  
Z. B. die folgende Abfrage sucht die `request_id` und der aktuelle `status` für jede Abfrage, die wählt alle Spalten aus der `memberAddresses` Tabelle.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE ‘%SELECT * FROM db1..memberAddresses%’;  
```  
  
Nach der `request_id` wurde für eine Abfrage identifiziert, verwenden Sie die anderen Informationen in den `dm_pdw_exec_requests` -Tabelle ab, um herauszufinden, zur Verarbeitung der Abfrage, oder verwenden Sie [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) Anzeigen des Status der einzelnen Abfrage Schritte für die Ausführung der Abfrage.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
