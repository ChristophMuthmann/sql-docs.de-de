---
title: Konfigurieren eines Benutzers zum Erstellen und Verwalten von SQL Server-Agent-Aufträgen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7f5978050e90b80e2aba76b33abc8b7a0f29f8b0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie einen Benutzer zum Erstellen oder Ausführen von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträgen konfigurieren.  
  
-   **Vorbereitungen:**  [Sicherheit](#Security)  
  
-   **Konfigurieren eines Benutzers zum Erstellen und Verwalten von SQL Server-Agent-Aufträgen mit:**  [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Sicherheit  
Um einen Benutzer für das Erstellen oder Ausführen von Aufträgen des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents zu konfigurieren, müssen Sie zunächst einen vorhandenen SQL Server-Anmeldenamen oder eine msdb-Rolle einer der folgenden festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents in der msdb-Datenbank hinzufügen: SQLAgentUserRole, SQLAgentReaderRole oder SQLAgentOperatorRole.  
  
Standardmäßig können Mitglieder dieser Datenbankrollen ihre eigenen Auftragsschritte erstellen, die unter ihrem Konto ausgeführt werden. Falls Benutzer, die keine Administratoren sind, Aufträge ausführen möchten, mit denen andere Arten von Auftragsschritten ausgeführt werden (z. B. [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Pakete), benötigen sie Zugriff auf ein Proxykonto. Alle Mitglieder der festen Serverrolle sysadmin haben die Berechtigung zum Erstellen, Ändern und Löschen von Proxykonten. Weitere Informationen zu den Berechtigungen, die jeder dieser festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Datenbankrollen zugeordnet sind, finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
#### <a name="Permissions"></a>Berechtigungen  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
**So fügen Sie einer festen Datenbankrolle des SQL Server-Agents einen SQL-Anmeldenamen oder eine msdb-Rolle hinzu**  
  
1.  Erweitern Sie im **Objekt-Explorer**einen Server.  
  
2.  Erweitern Sie **Sicherheit**und anschließend **Anmeldungen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Anmeldenamen, den Sie der festen Datenbankrolle des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents hinzufügen möchten, und klicken Sie auf **Eigenschaften**.  
  
4.  Wählen Sie auf der Seite **Benutzerzuordnung** des Dialogfelds **Anmeldungseigenschaften** die Zeile aus, die **msdb**enthält.  
  
5.  Aktivieren Sie unter **Mitgliedschaft in Datenbankrolle für: msdb**das Kontrollkästchen für die entsprechende feste Datenbankrolle des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents.  
  
**So konfigurieren Sie ein Proxykonto zum Erstellen und Verwalten von Auftragsschritten des SQL Server-Agents**  
  
1.  Erweitern Sie im **Objekt-Explorer**einen Server.  
  
2.  Erweitern Sie **SQL Server-Agent**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Proxys** , und klicken Sie dann auf **Neuer Proxy**.  
  
4.  Geben Sie im Dialogfeld **Neues Proxykonto** auf der Seite **Allgemein** den Proxynamen, den Anmeldeinformationsnamen und eine Beschreibung für den neuen Proxy an. Beachten Sie, dass Sie Anmeldeinformationen erstellen müssen, bevor Sie ein Proxykonto des SQL Server-Agents erstellen. Weitere Informationen zum Erstellen von Anmeldeinformationen finden Sie unter [Vorgehensweise: Erstellen von Anmeldeinformationen (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/c1e77e91-2a69-40d9-b8b3-97cffc710586) und [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/en-us/d5e9ae69-41d9-4e46-b13d-404b88a32d9d).  
  
5.  Aktivieren Sie die entsprechenden Subsysteme für diesen Proxy.  
  
6.  Auf der Seite **Prinzipale** können Sie Anmeldenamen oder Rollen hinzufügen oder entfernen, um den Zugriff auf das Proxykonto zu erteilen oder zu entziehen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md)  
  
