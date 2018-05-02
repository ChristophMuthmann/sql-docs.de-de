---
title: Feste Datenbankrollen des SQL Server-Agents|Microsoft-Dokumente
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0315832b3ed7bbd16929e4384c9bdf40c13fbe85
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-agent-fixed-database-roles"></a>Feste Datenbankrollen des SQL Server-Agents
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verfügt über die folgenden festen **msdb** -Datenbankrollen, mit denen Administratoren den Zugriff auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent besser steuern können. In der folgenden Auflistung sind die Rollen von den niedrigsten bis hin zu den höchsten Zugriffsberechtigungen enthalten:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Wenn Benutzer, die nicht Mitglied einer dieser Rollen sind, mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]verbunden sind, ist der **SQL Server-Agent** -Knoten in Objekt-Explorer nicht sichtbar. Ein Benutzer muss Mitglied einer dieser festen Datenbankrollen oder der festen **sysadmin** -Serverrolle sein, um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwenden zu können.  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Berechtigungen der festen Datenbankrollen des SQL Server-Agents  
Die Datenbankrollen-Berechtigungen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents stehen konzentrisch zueinander in Beziehung: Rollen mit höheren Berechtigungen erben die Berechtigungen der Rollen mit niedrigeren Berechtigungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Objekte (einschließlich Warnungen, Operatoren, Aufträge, Zeitpläne und Proxys). Wenn z. B. Mitglieder der Rolle **SQLAgentUserRole** mit den niedrigsten Berechtigungen Zugriff auf „proxy_A“ haben, haben die Mitglieder von **SQLAgentReaderRole** und **SQLAgentOperatorRole** automatisch Zugriff auf diesen Proxy, selbst wenn ihnen der Zugriff auf „proxy_A“ nicht ausdrücklich erteilt wurde. Dies kann zu Sicherheitsrisiken führen, die in den folgenden Abschnitten zu den einzelnen Rollen erläutert werden.  
  
### <a name="sqlagentuserrole-permissions"></a>SQLAgentUserRole-Berechtigungen  
**SQLAgentUserRole** ist die feste Datenbankrolle des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents mit den niedrigsten Berechtigungen. Sie hat lediglich Berechtigungen für Operatoren, lokale Aufträge und Auftragszeitpläne. Die Mitglieder von **SQLAgentUserRole** haben lediglich Berechtigungen für lokale Aufträge und Auftragszeitpläne, deren Besitzer sie sind. Sie können keine Multiserveraufträge (Master- und Zielserveraufträge) verwenden, und sie können den Auftragsbesitz nicht ändern, um Zugriff auf Aufträge zu erhalten, deren Besitzer sie nicht bereits sind. Die Mitglieder von**SQLAgentUserRole** können lediglich im Dialogfeld **Auftragsschritt-Eigenschaften** von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]eine Liste mit vorhandenen Proxys anzeigen. Nur der Knoten **Aufträge** in Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ist für die Mitglieder von **SQLAgentUserRole** sichtbar.  
  
> [!IMPORTANT]  
> Beachten Sie die Sicherheitsrisiken, bevor Sie den Mitgliedern **der**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-**Agent-Datenbankrollen** Proxyzugriff erteilen. **SQLAgentReaderRole** und **SQLAgentOperatorRole** sind automatisch Mitglieder von **SQLAgentUserRole**. Dies bedeutet, dass die Mitglieder von **SQLAgentReaderRole** und **SQLAgentOperatorRole** Zugriff auf alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxys haben, die **SQLAgentUserRole** erteilt wurden und diese Proxys verwenden können.  
  
Die folgende Tabelle enthält einen Überblick über die **SQLAgentUserRole** -Berechtigungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Objekte.  
  
|Aktion|Operatoren|Lokale Aufträge<br /><br />(nur Aufträge mit Besitzern)|Auftragszeitpläne<br /><br />(nur Zeitpläne mit Besitzern)|Proxys|  
|----------|-------------|-----------------------------------|-------------------------------------------|-----------|  
|Erstellen/Ändern/Löschen|nein|ja<br /><br />Der Auftragsbesitz kann nicht geändert werden.|ja|nein|  
|Liste anzeigen (aufzählen)|ja<br /><br />Die Liste mit verfügbaren Operatoren kann zum Verwenden in **sp_notify_operator** und im Dialogfeld **Auftragseigenschaften** von Management Studio abgerufen werden.|ja|ja|ja<br /><br />Die Liste der Proxys steht nur im Dialogfeld **Auftragsschritt-Eigenschaften** von Management Studio zur Verfügung.|  
|Aktivieren/Deaktivieren|nein|ja|ja|Nicht verfügbar|  
|Eigenschaften anzeigen|nein|ja|ja|nein|  
|Ausführen/Beenden/Starten|Nicht verfügbar|ja|Nicht verfügbar|Nicht verfügbar|  
|Auftragsverlauf anzeigen|Nicht verfügbar|ja|Nicht verfügbar|Nicht verfügbar|  
|Auftragsverlauf löschen|Nicht verfügbar|nein<br /><br />Den Mitgliedern von **SQLAgentUserRole** muss die EXECUTE-Berechtigung für **sp_purge_jobhistory** zum Löschen des Auftragsverlaufs für Aufträge, deren Besitzer sie sind, ausdrücklich erteilt werden. Sie können den Auftragsverlauf für keine anderen Aufträge löschen.|Nicht verfügbar|Nicht verfügbar|  
|Anfügen/Trennen|Nicht verfügbar|Nicht verfügbar|ja|Nicht verfügbar|  
  
### <a name="sqlagentreaderrole-permissions"></a>SQLAgentReaderRole-Berechtigungen  
**SQLAgentReaderRole** enthält alle **SQLAgentUserRole** -Berechtigungen sowie die Berechtigungen zum Anzeigen der Liste verfügbarer Multiserveraufträge, ihrer Eigenschaften und ihres Verlaufs. Die Mitglieder dieser Rolle können auch die Liste aller verfügbaren Aufträge und Auftragszeitpläne sowie ihre Eigenschaften anzeigen, nicht nur die Aufträge und Auftragszeitpläne, deren Besitzer sie sind. Die Mitglieder von**SQLAgentReaderRole** können den Auftragsbesitz nicht ändern, um Zugriff auf Aufträge zu erhalten, deren Besitzer sie nicht bereits sind. Nur der Knoten **Aufträge** in Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ist für die Mitglieder von **SQLAgentReaderRole** sichtbar.  
  
> [!IMPORTANT]  
> Beachten Sie die Sicherheitsrisiken, bevor Sie den Mitgliedern **der**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-**Agent-Datenbankrollen** Proxyzugriff erteilen. Die Mitglieder von **SQLAgentReaderRole** sind automatisch auch Mitglieder von **SQLAgentUserRole**. Dies bedeutet, dass die Mitglieder von **SQLAgentReaderRole** Zugriff auf alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxys haben, die **SQLAgentUserRole** erteilt wurden und diese Proxys verwenden können.  
  
Die folgende Tabelle enthält einen Überblick über die **SQLAgentReaderRole** -Berechtigungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Objekte.  
  
|Aktion|Operatoren|Lokale Aufträge|Multiserveraufträge|Auftragszeitpläne|Proxys|  
|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Erstellen/Ändern/Löschen|nein|Ja (nur Aufträge mit Besitzer)<br /><br />Der Auftragsbesitz kann nicht geändert werden.|nein|Ja (nur Zeitpläne mit Besitzer)|nein|  
|Liste anzeigen (aufzählen)|ja<br /><br />Die Liste mit verfügbaren Operatoren kann zum Verwenden in **sp_notify_operator** und im Dialogfeld **Auftragseigenschaften** von Management Studio abgerufen werden.|ja|ja|ja|ja<br /><br />Die Liste der Proxys steht nur im Dialogfeld **Auftragsschritt-Eigenschaften** von Management Studio zur Verfügung.|  
|Aktivieren/Deaktivieren|nein|Ja (nur Aufträge mit Besitzer)|nein|Ja (nur Zeitpläne mit Besitzer)|Nicht verfügbar|  
|Eigenschaften anzeigen|nein|ja|ja|ja|nein|  
|Eigenschaften bearbeiten|nein|Ja (nur Aufträge mit Besitzer)|nein|Ja (nur Zeitpläne mit Besitzer)|nein|  
|Ausführen/Beenden/Starten|Nicht verfügbar|Ja (nur Aufträge mit Besitzer)|nein|Nicht verfügbar|Nicht verfügbar|  
|Auftragsverlauf anzeigen|Nicht verfügbar|ja|ja|Nicht verfügbar|Nicht verfügbar|  
|Auftragsverlauf löschen|Nicht verfügbar|nein<br /><br />Den Mitgliedern von **SQLAgentReaderRole** muss die EXECUTE-Berechtigung für **sp_purge_jobhistory** zum Löschen des Auftragsverlaufs für Aufträge, deren Besitzer sie sind, ausdrücklich erteilt werden. Sie können den Auftragsverlauf für keine anderen Aufträge löschen.|nein|Nicht verfügbar|Nicht verfügbar|  
|Anfügen/Trennen|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Ja (nur Zeitpläne mit Besitzer)|Nicht verfügbar|  
  
### <a name="sqlagentoperatorrole-permissions"></a>SQLAgentOperatorRole-Berechtigungen  
**SQLAgentOperatorRole** ist die feste Datenbankrolle des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents mit den höchsten Berechtigungen. Sie enthält alle Berechtigungen von **SQLAgentUserRole** und **SQLAgentReaderRole**. Die Mitglieder dieser Rolle können auch die Eigenschaften für Operatoren und Proxys anzeigen und die verfügbaren Proxys und Warnungen auf dem Server aufzählen.  
  
Die Mitglieder von**SQLAgentOperatorRole** haben zusätzliche Berechtigungen für lokale Aufträge und Zeitpläne. Sie können alle lokalen Aufträge ausführen, beenden oder starten, und sie können den Auftragsverlauf eines lokalen Auftrags auf dem Server löschen. Sie können auch alle lokalen Aufträge und Zeitpläne auf dem Server aktivieren und deaktivieren. Um lokale Aufträge oder Zeitpläne zu aktivieren oder zu deaktivieren, müssen die Mitglieder dieser Rolle die gespeicherten Prozeduren **sp_update_job** und **sp_update_schedule**verwenden. Nur die Parameter, die den Namen oder den Bezeichner des Auftrags oder Zeitplans sowie den **@enabled** -Parameter angeben, können von den Mitgliedern von **SQLAgentOperatorRole**eine Liste mit vorhandenen Proxys anzeigen. Wenn sie andere Parameter angeben, erzeugt die Ausführung dieser gespeicherten Prozeduren einen Fehler. Die Mitglieder von**SQLAgentOperatorRole** können den Auftragsbesitz nicht ändern, um Zugriff auf Aufträge zu erhalten, deren Besitzer sie nicht bereits sind.  
  
Die Knoten **Aufträge**, **Warnungen**, **Operatoren**und **Proxys** in Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] sind für die Mitglieder von **SQLAgentOperatorRole**sichtbar. Nur der Knoten **Fehlerprotokolle** ist für die Mitglieder dieser Rolle nicht sichtbar.  
  
> [!IMPORTANT]  
> Beachten Sie die Sicherheitsrisiken, bevor Sie den Mitgliedern **der**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-**Agent-Datenbankrollen** Proxyzugriff erteilen. Die Mitglieder von **SQLAgentOperatorRole** sind automatisch auch Mitglieder von **SQLAgentUserRole** und **SQLAgentReaderRole**. Dies bedeutet, dass die Mitglieder von **SQLAgentOperatorRole** Zugriff auf alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxys haben, die **SQLAgentUserRole** oder **SQLAgentReaderRole** erteilt wurden und diese Proxys verwenden können.  
  
Die folgende Tabelle enthält einen Überblick über die **SQLAgentOperatorRole** -Berechtigungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Objekte.  
  
|Aktion|Warnungen|Operatoren|Lokale Aufträge|Multiserveraufträge|Auftragszeitpläne|Proxys|  
|----------|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Erstellen/Ändern/Löschen|nein|nein|Ja (nur Aufträge mit Besitzer)<br /><br />Der Auftragsbesitz kann nicht geändert werden.|nein|Ja (nur Zeitpläne mit Besitzer)|nein|  
|Liste anzeigen (aufzählen)|ja|ja<br /><br />Die Liste mit verfügbaren Operatoren kann zum Verwenden in **sp_notify_operator** und im Dialogfeld **Auftragseigenschaften** von Management Studio abgerufen werden.|ja|ja|ja|ja|  
|Aktivieren/Deaktivieren|nein|nein|ja<br /><br />**SQLAgentOperatorRole** können lokale Aufträge, deren Besitzer sie nicht sind, aktivieren oder deaktivieren, indem sie die gespeicherte Prozedur **sp_update_job** verwenden und Werte für die **@enabled** und **@job_id** -Parameter (oder **@job_name**) angeben. Wenn ein Mitglied dieser Rolle einen anderen Parameter für diese gespeicherte Prozedur angibt, erzeugt die Ausführung der Prozedur einen Fehler.|nein|ja<br /><br />**SQLAgentOperatorRole** können Zeitpläne, deren Besitzer sie nicht sind, aktivieren oder deaktivieren, indem sie die gespeicherte Prozedur **sp_update_schedule** verwenden und Werte für die **@enabled** und **@schedule_id** -Parameter (oder **@name**) angeben. Wenn ein Mitglied dieser Rolle einen anderen Parameter für diese gespeicherte Prozedur angibt, erzeugt die Ausführung der Prozedur einen Fehler.|Nicht verfügbar|  
|Eigenschaften anzeigen|ja|ja|ja|ja|ja|ja|  
|Eigenschaften bearbeiten|nein|nein|Ja (nur Aufträge mit Besitzer)|nein|Ja (nur Zeitpläne mit Besitzer)|nein|  
|Ausführen/Beenden/Starten|Nicht verfügbar|Nicht verfügbar|ja|nein|Nicht verfügbar|Nicht verfügbar|  
|Auftragsverlauf anzeigen|Nicht verfügbar|Nicht verfügbar|ja|ja|Nicht verfügbar|Nicht verfügbar|  
|Auftragsverlauf löschen|Nicht verfügbar|Nicht verfügbar|ja|nein|Nicht verfügbar|Nicht verfügbar|  
|Anfügen/Trennen|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Ja (nur Zeitpläne mit Besitzer)|Nicht verfügbar|  
  
## <a name="assigning-users-multiple-roles"></a>Zuweisen von mehreren Rollen an Benutzer  
Die Mitglieder der festen Serverrolle **sysadmin** haben Zugriff auf alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Funktionen. Wenn ein Benutzer nicht Mitglied der **sysadmin** -Rolle ist, sondern von mehr als einer festen Datenbankrolle des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents, sollten Sie das konzentrische Berechtigungsmodell dieser Rollen berücksichtigen. Da die Rollen mit höheren Berechtigungen immer alle Berechtigungen der Rollen mit niedrigeren Berechtigungen enthalten, hat ein Benutzer, der Mitglied von mehreren Rollen ist, automatisch die Berechtigungen der Rolle mit den höchsten Berechtigungen, deren Mitglied der Benutzer ist.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md)  
[sp_update_job (Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623)  
[sp_update_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/97b3119b-e43e-447a-bbfb-0b5499e2fefe)  
[sp_notify_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/c440f5c9-9884-4196-b07c-55d87afb17c3)  
[sp_purge_jobhistory (Transact-SQL)](http://msdn.microsoft.com/en-us/237f9bad-636d-4262-9bfb-66c034a43e88)  
  
