---
title: "Aktivieren oder Deaktivieren der Datensammlung | Microsoft Docs"
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
  - "Datensammler [SQL Server], deaktivieren"
  - "Datensammler [SQL Server], aktivieren"
ms.assetid: 0137971b-fb48-4a3e-822a-3df2b9bb09d7
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Aktivieren oder Deaktivieren der Datensammlung
  In diesem Thema wird beschrieben, wie die Datensammlung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]aktiviert oder deaktiviert wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So aktivieren oder deaktivieren Sie die Datensammlung mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle **dc_admin** oder **dc_operator** (mit EXECUTE-Berechtigung) erforderlich.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So aktivieren Sie den Datensammler  
  
1.  Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung** .  
  
2.  Klicken Sie mit der rechten Maustaste auf **Datensammlung**, und klicken Sie anschließend auf **Datensammlung aktivieren**.  
  
#### So deaktivieren Sie den Datensammler  
  
1.  Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung** .  
  
2.  Klicken Sie mit der rechten Maustaste auf **Datensammlung**, und klicken Sie anschließend auf **Datensammlung deaktivieren**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So aktivieren Sie den Datensammler  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird der Datensammler mithilfe von [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) aktiviert.  
  
```tsql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector ;  
```  
  
#### So deaktivieren Sie den Datensammler  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird der Datensammler mithilfe von [sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md) deaktiviert.  
  
```tsql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## Siehe auch  
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  