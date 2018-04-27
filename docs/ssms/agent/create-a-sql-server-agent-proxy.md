---
title: Erstellen eines Proxys für den SQL Server-Agent | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/04/2017
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
- proxies [SQL Server Agent], creating
ms.assetid: 142e0c55-a8b9-4669-be49-b9dc602d5988
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0e23c0afe1c33411e53b9e072625b84c6a19431c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-sql-server-agent-proxy"></a>Erstellen eines Proxys für den SQL Server-Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie SQL Server-Agent-Proxys in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]erstellt werden.  
  
Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxykonto definiert einen Sicherheitskontext, in dem ein Auftragsschritt ausgeführt werden kann. Jeder Proxy entspricht Sicherheitsanmeldeinformationen. Um Berechtigungen für einen bestimmten Auftragsschritt festzulegen, erstellen Sie ein Proxykonto mit den erforderlichen Berechtigungen für ein Subsystem des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents und weisen dann dieses Proxykonto dem Auftragsschritt zu.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So erstellen Sie einen Proxy für den SQL Server-Agent mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   Sie müssen, falls keine Anmeldeinformationen vorhanden sind, Anmeldeinformationen erstellen, bevor Sie ein Proxykonto erstellen.  
  
-   Von[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxys werden Anmeldeinformationen zum Speichern von Informationen zu Windows-Benutzerkonten verwendet. Der in den Anmeldeinformationen angegebene Benutzer muss über die Berechtigung „Access this computer from the network (Auf diesen Computer vom Netzwerk zugreifen)“ (SeNetworkLogonRight) auf dem Computer verfügen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent wird der Subsystemzugriff für einen Proxy überprüft und der Zugriff auf den Proxy jedes Mal dann gewährt, wenn der Auftragsschritt ausgeführt wird. Wenn der Proxyzugriff auf das Subsystem nicht mehr länger möglich ist, erzeugt der Auftragsschritt einen Fehler. Ansonsten wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die Identität des Benutzers angenommen, der im Proxy angegeben ist und von dem der Auftragsschritt ausgeführt wird.  
  
-   Die Berechtigungen für den Benutzer werden nicht durch das Erstellen eines Proxys geändert, der in den Anmeldeinformationen für den Proxy angegeben ist. Sie können beispielsweise einen Proxy für einen Benutzer erstellen, der keine Verbindungsberechtigung für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]hat. In diesem Fall kann von Auftragsschritten, die diesen Proxy verwenden, keine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]hergestellt werden.  
  
-   Wenn die Anmeldung für den Benutzer Zugriffsrecht auf den Proxy hat, oder der Benutzer zu einer Rolle mit Zugriffsrechten auf den Proxy gehört, kann der Benutzer den Proxy in einem Auftragsschritt verwenden.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
  
-   Nur Mitglieder der festen Serverrolle **sysadmin** haben die Berechtigung zum Erstellen, Ändern oder Löschen von Proxykonten. Benutzer, die nicht Mitglieder der festen Serverrolle **sysadmin** sind, müssen zur Verwendung von Proxys einer der folgenden festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents in der **msdb** -Datenbank hinzugefügt werden: **SQLAgentUserRole**, **SQLAgentReaderRole**oder **SQLAgentOperatorRole**.  
  
-   Erfordert die **ALTER ANY CREDENTIAL** -Berechtigung, wenn für den Proxy zusätzlich eine Anmeldeinformation erstellt wird.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>So erstellen Sie einen Proxy für den SQL Server-Agent  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, auf dem Sie ein Proxy auf dem SQL Server-Agent erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Proxys** , und wählen Sie dann **Neuer Proxy**aus.  
  
4.  Geben Sie in das Dialogfeld **Neues Proxykonto** auf der Seite **Allgemein** den Namen des neuen Proxykontos in das Feld **Proxyname** ein.  
  
5.  Geben Sie im Feld **Anmeldeinformationsname** den Namen der Sicherheitsanmeldeinformationen ein, die vom Proxykonto verwendet werden.  
  
6.  Geben Sie im Feld **Beschreibung** eine Beschreibung für das Proxykonto ein.  
  
7.  Wählen Sie unter **Folgenden Subsystemen gegenüber aktiv**das bzw. die entsprechenden Subsysteme für diesen Proxy aus.  
  
8.  Auf der Seite **Prinzipale** können Sie Anmeldenamen oder Rollen hinzufügen oder entfernen, um den Zugriff auf das Proxykonto zu erteilen oder zu entziehen.  
  
9. Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>So erstellen Sie einen Proxy für den SQL Server-Agent  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- creates credential CatalogApplicationCredential  
    USE msdb ;  
    GO  
    CREATE CREDENTIAL CatalogApplicationCredential WITH IDENTITY = 'REDMOND/TestUser',   
        SECRET = 'G3$1o)lkJ8HNd!';  
    GO  
    -- creates proxy "Catalog application proxy" and assigns
    -- the credential 'CatalogApplicationCredential' to it.  
    EXEC dbo.sp_add_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 1,  
        @description = 'Maintenance tasks on catalog application.',  
        @credential_name = 'CatalogApplicationCredential' ;  
    GO  
    -- grants the proxy "Catalog application proxy" access to 
    -- the ActiveX Scripting subsystem.  
    EXEC dbo.sp_grant_proxy_to_subsystem  
        @proxy_name = N'Catalog application proxy',  
        @subsystem_id = 2 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/en-us/d5e9ae69-41d9-4e46-b13d-404b88a32d9d)  
  
-   [sp_add_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/cb59df37-f103-439b-bec1-2871fb669a8b)  
  
-   [sp_grant_proxy_to_subsystem (Transact-SQL)](http://msdn.microsoft.com/en-us/866aaa27-a1e0-453a-9b1b-af39431ad9c2)  
  
