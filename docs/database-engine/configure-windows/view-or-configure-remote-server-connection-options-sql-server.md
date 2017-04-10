---
title: "Anzeigen oder Konfigurieren von Verbindungsoptionen f&#252;r Remoteserver (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Remoteserver [SQL Server], Verbindungsoptionen"
  - "Server [SQL Server], Remote"
  - "Verbindungen [SQL Server], Remoteserver"
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Anzeigen oder Konfigurieren von Verbindungsoptionen f&#252;r Remoteserver (SQL Server)
  In diesem Thema wird beschrieben, wie Sie Verbindungsoptionen für Remoteserver auf Serverebene in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]anzeigen oder konfigurieren können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie Verbindungsoptionen für Remoteserver an oder konfigurieren sie mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren von Verbindungsoptionen für Remoteserver](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Für das Ausführen von **sp_serveroption** sind ALTER ANY LINKED SERVER-Berechtigungen auf dem Server erforderlich.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So zeigen Sie Verbindungsoptionen für Remoteserver an oder konfigurieren sie  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **SQL Server-Eigenschaften - \<***Servername***>** auf **Verbindungen**.  
  
3.  Überprüfen Sie auf der Seite **Verbindungen** die Einstellungen für **Remoteserververbindungen** , und ändern Sie sie gegebenenfalls.  
  
4.  Wiederholen Sie Schritt 1 bis 3 auf dem zweiten Server des Remoteserverpaares.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So zeigen Sie Verbindungsoptionen für Remoteserver an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel werden von [sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md) Informationen über alle Remoteserver zurückgegeben.  
  
```tsql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### So konfigurieren Sie Verbindungsoptionen für Remoteserver  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_serveroption](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md) zum Konfigurieren eines Remoteservers verwendet wird. In diesem Beispiel wird ein Remoteserver, der einer anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz (`SEATTLE3`) entspricht, so konfiguriert, dass seine Sortierung mit der Sortierung der lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz kompatibel ist.  
  
```tsql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren von Verbindungsoptionen für Remoteserver  
 Der Remoteserver muss angehalten und neu gestartet werden, damit die Einstellung wirksam werden kann.  
  
## Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Remoteserver](../../database-engine/configure-windows/remote-servers.md)   
 [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  