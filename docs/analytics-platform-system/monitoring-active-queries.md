---
title: "Überwachen von aktiven Abfragen (SQLServer PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb73f790-0537-414b-8dc2-f1eb69b92362
caps.latest.revision: "7"
ms.openlocfilehash: 44f128124c8027bf4c37e34309d6c711006ac113
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="monitoring-active-queries"></a>Überwachen von aktiven Abfragen
In diesem Thema wird gezeigt, wie die-Verwaltungskonsole und die SQL Server PDW-Systemsichten zu verwenden, um aktive Abfragen zu überwachen. Finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole](monitor-the-appliance-by-using-the-admin-console.md) und [Systemsichten](tsql-system-views.md) Informationen zu diesen Tools.  
  
## <a name="prerequisites"></a>Voraussetzungen  
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
  
