---
title: Löschen eines SQL Server-Agent-Proxys | Microsoft-Dokumentation
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
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 74e7c53e0122c539fdc86cf3a7bca39a3881e5b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="delete-a-sql-server-agent-proxy"></a>Delete a SQL Server Agent Proxy
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxykonto in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]löschen können.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So löschen Sie einen SQL Server-Agent-Proxykonto mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   Wenn Sie das Proxykonto eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents löschen, sollten Sie sicherstellen, dass der Proxy keine Verweise auf aktive Auftragsschritte enthält. Klicken Sie mit der rechten Maustaste auf den Proxy, um nach Auftragsschritten zu suchen, die auf den Proxy verweisen. Klicken Sie zuerst auf **Eigenschaften** und dann im Dialogfeld *Proxyname***Eigenschaften von Proxykonto* auf die Seite **Verweise**. Beim Löschen eines Proxys können Sie im Dialogfeld **Objekt löschen** die Auftragsschritte, die diesen Proxy verwenden, neu zuweisen.  
  
-   Von[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxys werden Anmeldeinformationen zum Speichern von Informationen zu Windows-Benutzerkonten verwendet. Der in der Anmeldeinformation angegebene Benutzer muss über eine Berechtigung des Typs "Anmelden als Stapelverarbeitungsauftrag" auf dem Computer verfügen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent wird der Subsystemzugriff für einen Proxy überprüft und der Zugriff auf den Proxy jedes Mal dann gewährt, wenn der Auftragsschritt ausgeführt wird. Wenn der Proxyzugriff auf das Subsystem nicht mehr länger möglich ist, erzeugt der Auftragsschritt einen Fehler. Ansonsten wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die Identität des Benutzers angenommen, der im Proxy angegeben ist und von dem der Auftragsschritt ausgeführt wird.  
  
-   Wenn die Anmeldung für den Benutzer Zugriffsrecht auf den Proxy hat, oder der Benutzer zu einer Rolle mit Zugriffsrechten auf den Proxy gehört, kann der Benutzer den Proxy in einem Auftragsschritt verwenden.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Nur Mitglieder der festen Serverrolle **sysadmin** können Proxykonten erstellen, ändern oder löschen.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>So löschen Sie ein SQL Server-Agent-Proxykonto  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, der das Proxykonto enthält, das Sie löschen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um den Ordner **Proxys** zu erweitern.  
  
4.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um das Subsystem zu erweitern, das das zu löschende Proxykonto enthält (z. B. **ActiveX-Skript**).  
  
5.  Klicken Sie mit der rechten Maustaste auf das Proxykonto, das Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
6.  Bestätigen Sie im Dialogfeld **Objekt löschen** , dass das richtige Proxykonto ausgewählt ist. Aktivieren Sie das Kontrollkästchen **Neu zuweisen an** , um die Auftragsschritte, die auf dieses Proxykonto verweisen, einem anderen Proxykonto zuzuweisen.  
  
7.  Klicken Sie auf **OK**.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>So löschen Sie ein SQL Server-Agent-Proxykonto  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_delete_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/44a1db13-b7f2-4dab-a1b5-b8dafb41737c).  
  
