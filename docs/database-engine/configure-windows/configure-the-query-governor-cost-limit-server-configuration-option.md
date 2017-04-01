---
title: "Konfigurieren der Serverkonfigurationsoption Kostenbeschr&#228;nkung der Abfragekontrolle | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abfragen [SQL Server], Ausführungszeit"
  - "Kostenbeschränkung der Abfragekontrolle (Option) [SQL Server]"
  - "Zeit [SQL Server], Uhrzeit der Abfrageausführung"
ms.assetid: e7b8f084-1052-4133-959b-cebf4add790f
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Konfigurieren der Serverkonfigurationsoption Kostenbeschr&#228;nkung der Abfragekontrolle
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Kostenbeschränkung der Abfragekontrolle** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Die Kostenbeschränkungsoption der Abfragekontrolle legt ein Höchstlimit für den Zeitraum an, in dem eine Abfrage ausgeführt werden kann. Die Abfragekosten beziehen sich auf eine geschätzte Zeit in Sekunden, die für das Ausführen einer Abfrage bei einer bestimmten Hardwarekonfiguration benötigt wird. Der Standardwert für diese Option ist 0, mit dem die Abfragekontrolle deaktiviert wird. Alle Abfragen können dann ohne zeitliche Begrenzung ausgeführt werden. Wenn Sie einen nicht negativen Wert ungleich Null angeben, lässt die Abfragekontrolle die Ausführung von Abfragen nicht zu, deren geschätzte Kosten über diesem Wert liegen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option Kostenbeschränkung der Abfragekontrolle mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:** [Nach dem Konfigurieren der Option Kostenbeschränkung der Abfragekontrolle](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Techniker geändert werden.  
  
-   Wenn Sie den Wert der Option Kostenbeschränkung der Abfragekontrolle jeweils für eine Verbindung ändern möchten, können Sie dazu die [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)-Anweisung verwenden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So konfigurieren Sie die Option Kostenbeschränkung der Abfragekontrolle  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften** aus.  
  
2.  Klicken Sie auf die Seite **Verbindungen** .  
  
3.  Aktivieren bzw. deaktivieren Sie das Kontrollkästchen **Abfragekontrolle verwenden, um Abfragen mit langer Ausführungszeit zu verhindern**.  
  
     Wenn Sie dieses Kontrollkästchen aktivieren, geben Sie in das untere Feld einen positiven Wert ein, der von der Abfragekontrolle verwendet wird, um das Ausführen von Abfragen nicht zuzulassen, deren Ausführungszeiten diesen Wert überschreiten.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So konfigurieren Sie die Option Kostenbeschränkung der Abfragekontrolle  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `query governor cost limit` auf `120` Sekunden festzulegen.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'query governor cost limit', 120 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Kostenbeschränkung der Abfragekontrolle  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  