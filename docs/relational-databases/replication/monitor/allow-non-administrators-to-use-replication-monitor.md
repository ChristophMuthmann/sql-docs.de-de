---
title: "Zulassen, dass Nichtadministratoren den Replikationsmonitor verwenden | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Replikationsmonitor, Zugriff durch Nichtadministratoren"
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Zulassen, dass Nichtadministratoren den Replikationsmonitor verwenden
  In diesem Thema wird beschrieben, wie Nicht-Administratoren ermöglicht wird, den Replikationsmonitor in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] zu verwenden. Der Replikationsmonitor kann von Benutzern verwendet werden, die Mitglieder der folgenden Rollen sind:  
  
-   Feste Serverrolle **sysadmin** .  
  
     Diese Benutzer können die Replikation überwachen und haben den vollen Zugriff in Bezug auf Änderungen der Replikationseigenschaften, wie beispielsweise Zeitpläne für Agents, Agentprofile usw.  
  
-   Datenbankrolle **replmonitor** in der Verteilungsdatenbank.  
  
     Diese Benutzer können die Replikation überwachen, aber keine Replikationseigenschaften ändern.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So ermöglichen Sie Nichtadministratoren die Verwendung des Replikationsmonitors mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Nichtadministratoren den Replikationsmonitor, Mitglied verwenden sollen die **Sysadmin** festen Serverrolle fügen Sie den Benutzer an die Verteilungsdatenbank und weisen Sie diesem Benutzer muss die **Replmonitor** Rolle.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So lassen Sie zu, dass Nichtadministratoren den Replikationsmonitor verwenden  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie **Datenbanken**, erweitern Sie **Systemdatenbanken**, und erweitern Sie dann die Verteilungsdatenbank (mit dem Namen **Verteilung** standardmäßig).  
  
3.  Erweitern Sie **Sicherheit**, mit der rechten Maustaste **Benutzer**, und klicken Sie dann auf **Neuer Benutzer**.  
  
4.  Geben Sie einen Benutzernamen und ein Kennwort für den Benutzer ein.  
  
5.  Wählen Sie ein Standardschema für **replmonitor**aus.  
  
6.  Aktivieren Sie das Kontrollkästchen **replmonitor** im Raster **Mitglied in Datenbankrollen** .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So fügen Sie der festen Datenbankrolle "replmonitor" einen Benutzer hinzu  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_helpuser & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md). Wenn der Benutzer nicht, in aufgeführt ist **Benutzername** im Resultset, der Benutzer muss Zugriff auf die Verteilung mithilfe der [CREATE USER & #40; Transact-SQL & #41;](../../../t-sql/statements/create-user-transact-sql.md) -Anweisung.  
  
2.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_helprolemember & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), Angabe des Werts **Replmonitor** für die **@rolename** Parameter. Wenn der Benutzer unter **MemberName** im Resultset aufgeführt wird, gehört der Benutzer bereits zu der Rolle.  
  
3.  Wenn der Benutzer nicht zu gehört die **Replmonitor** Rolle ausführen [Sp_addrolemember & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank. Geben Sie einen Wert **replmonitor** für **@rolename** und den Namen des Datenbankbenutzers oder den [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows login being added für **@membername**.  
  
#### So entfernen Sie einen Benutzer aus der festen Datenbankrolle "replmonitor"  
  
1.  Um sicherzustellen, dass der Benutzer gehört die **Replmonitor** Rolle ausführen [Sp_helprolemember & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank und geben Sie den Wert **Replmonitor** für **@rolename**. Wenn der Benutzer unter **MemberName** im Resultset nicht aufgeführt wird, gehört der Benutzer aktuell nicht zu der Rolle.  
  
2.  Gehört der Benutzer an die **Replmonitor** Rolle ausführen [Sp_droprolemember & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank. Geben Sie den Wert **replmonitor** für **@rolename** und den Namen des Datenbankbenutzers oder den Windows-Anmeldenamen an, der für **@membername**entfernt wird.  
  
  