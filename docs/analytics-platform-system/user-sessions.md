---
title: Benutzersitzungen (SQLServer PDW)
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
ms.assetid: 0425cef2-de4d-4f42-91c5-cb1cd4bb1265
caps.latest.revision: "15"
ms.openlocfilehash: ca67e05e5dc087da683109d498c45672720cd2f9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="user-sessions"></a>Benutzersitzungen
Eine Anmeldung mit den entsprechenden Berechtigungen können Sie die Sitzungen aller Anmeldenamen auf einer SQL Server PDW Appliance, einschließlich Ausführen dieser Aktionen verwalten:  
  
-   Zeigen Sie die aktuellen Sitzungen auf dem Gerät, einschließlich aktive und im Leerlauf Sitzungen an.  
  
-   Zeigt die aktiven und aktuellen Abfragen für eine Sitzung an.  
  
-   Aktive Sitzungen zu beenden.  
  
Diese Aktionen können ausgeführt werden, indem Sie entweder die [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole](monitor-the-appliance-by-using-the-admin-console.md) oder [Systemsichten](tsql-system-views.md) über SQL-Befehlen, wie unten dargestellt.  
  
Die erforderlichen Berechtigungen zum Sitzungen zu verwalten, indem Sie mit beiden Methoden sind identisch und werden in beschrieben [Erteilen von Berechtigungen zum Verwalten von Anmeldungen, Benutzer und Datenbankrollen](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Verwalten von Sitzungen mit der Verwaltungskonsole  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>So zeigen Sie die aktuelle Sitzungen mithilfe der Verwaltungskonsole  
  
1.  Klicken Sie im oberen Menü auf **Sitzungen**.  
  
2.  Die resultierende Liste zeigt alle aktuellen Sitzungen an. Um nur die Sitzungen "Aktiv" oder "Leerlauf" anzuzeigen, klicken Sie auf die **Status** Spaltenüberschrift zum Sortieren der Ergebnisse nach Status.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>So zeigen Sie mithilfe der Verwaltungskonsole für eine Sitzung aktive und aktuelle Abfragen  
  
1.  Klicken Sie im oberen Menü auf **Sitzungen**.  
  
2.  Klicken Sie auf die Sitzungs-ID der gewünschten Sitzung, in der Ergebnisliste.  
  
3.  Die Ergebnisliste Abfragen zeigt die aktuellen Abfragen für die Sitzung. Informationen zum Anzeigen von Abfragedetails finden Sie unter [aktive Abfragen Überwachung](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Um Sitzungen zu beenden, mithilfe der Verwaltungskonsole  
  
1.  Klicken Sie im oberen Menü auf **Sitzungen**.  
  
2.  Suchen Sie die Sitzungs-ID für die Sitzung auf "Abbrechen".  
  
3.  Klicken Sie auf das rote **X** links neben die Sitzungs-ID zum Beenden der Sitzung. Nur Sitzungen mit dem Status 'Aktiv' oder 'Im Leerlauf' einen roten **X**; nur diese Sitzungen beendet werden können.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Verwalten von Sitzungen mit Systemsichten und SQL-Befehle  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Zum Anzeigen der aktuellen Sitzungen mithilfe von Systemsichten  
Verwendung [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) zum Generieren einer Liste aktueller Sitzungen an.  
  
In diesem Beispiel gibt die Session_id Login_name und Status für alle Sitzungen mit dem Status "Aktiv" oder "Leerlauf" zurück.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>So zeigen Sie aktive und aktuelle Abfragen für eine Sitzung mithilfe von Systemsichten  
Um die aktiven und abgeschlossenen Abfragen, die einer Sitzung zugeordneten anzuzeigen, verwenden Sie die [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) und [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) Ansichten. Diese Abfrage gibt eine Liste aller aktiven oder im Leerlauf Sitzungen sowie alle aktiven oder kürzlich erfolgten Abfragen, die jede Sitzungs-ID zugeordnet  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>Um Sitzungen zu beenden, mithilfe von SQL-Befehle  
Verwenden der [KILL](../t-sql/language-elements/kill-transact-sql.md) Befehl aus, um eine aktuelle Sitzung zu beenden. Sie benötigen die Sitzungs-ID für den Prozess zu beenden, die mit abgerufen werden können die [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) anzeigen.  
  
Wählen Sie in diesem Beispiel die Login_name, Session_id und Statuswerte finden Sie eine Sitzung, die basierend auf den Anmeldenamen ein.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
Sitzungen mit dem Status "Aktiv" oder "Leerlauf" können mithilfe des KILL-Befehls beendet werden.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
