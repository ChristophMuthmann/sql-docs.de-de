---
title: "Entfernen eines Steuerungspunkts f&#252;r das Hilfsprogramm (SQL Server-Hilfsprogramm) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c048a416-900e-4c77-8243-e0f0d8b94068
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Entfernen eines Steuerungspunkts f&#252;r das Hilfsprogramm (SQL Server-Hilfsprogramm)
  In diesem Thema wird beschrieben, wie Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Steuerungspunkt für das Hilfsprogramm (UCP) von der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] entfernen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So entfernen Sie einen Steuerungspunkt für das Hilfsprogramm mit**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Bevor Sie den UCP aus dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm entfernen, die folgenden Bedingungen erfüllt sein. Die gespeicherte Prozedur führt die erforderlichen Überprüfungen im Rahmen des Vorgangs aus.  
  
-   Vor dem Ausführen dieser Prozedur müssen alle verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus dem UCP entfernt werden. Beachten Sie dabei, dass der UCP eine verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist. Weitere Informationen finden Sie unter [Entfernen einer Instanz von SQL Server aus dem SQL Server-Hilfsprogramm](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
-   Diese Prozedur muss auf einem Computer ausgeführt werden, der ein UCP ist.  
  
-   Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aus der der UCP entfernt wurde, nur Datensammlungen enthält, die nicht von dem Hilfsprogramm stammen, wird die UMDW-Datenbank (sysutility_mdw) von der Prozedur nicht gelöscht. In diesem Fall muss die UMDW-Datenbank (sysutility_mdw) manuell gelöscht werden, bevor der UCP erneut erstellt werden kann.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Prozedur muss von einem Benutzer mit **sysadmin** -Berechtigungen ausgeführt werden, d. h. den gleichen Berechtigungen, die auch zum Erstellen eines UCP erforderlich sind.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So entfernen Sie einen Steuerungspunkt für das Hilfsprogramm  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
## Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Verwenden des Hilfsprogramm-Explorers zum Verwalten des SQL Server-Hilfsprogramms](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Problembehandlung beim SQL Server-Hilfsprogramm](../Topic/Troubleshoot%20the%20SQL%20Server%20Utility.md)  
  
  