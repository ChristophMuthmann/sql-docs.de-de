---
title: "Festlegen des Kompatibilit&#228;tsgrads von Mergever&#246;ffentlichungen | Microsoft Docs"
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
  - "Kompatibilität [SQL Server], Replikation"
  - "Abwärtskompatibilität [SQL Server], Replikation"
  - "Veröffentlichungen [SQL Server-Replikation], Abwärtskompatibilität"
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Festlegen des Kompatibilit&#228;tsgrads von Mergever&#246;ffentlichungen
  In diesem Thema wird beschrieben, wie der Kompatibilitätsgrad für Mergeveröffentlichungen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]festgelegt wird. Bei der Mergereplikation wird anhand des Kompatibilitätsgrades der Veröffentlichung bestimmt, welche Funktionen von Veröffentlichungen in der jeweiligen Datenbank verwendet werden können.  
  
 **In diesem Thema**  
  
-   **So legen Sie den Kompatibilitätsgrad von Mergeveröffentlichungen fest mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Der Kompatibilitätsgrad wird auf der Seite **Abonnententypen** des Assistenten für neue Veröffentlichung festgelegt. Weitere Informationen zum Zugreifen auf dieses Assistenten finden Sie unter [Erstellen einer Publikation](../../../relational-databases/replication/publish/create-a-publication.md). Nach dem Erstellen einer Veröffentlichungsmomentaufnahme kann der Kompatibilitätsgrad zwar erhöht, nicht aber gesenkt werden. Erhöhen Sie den Kompatibilitätsgrad auf die **Allgemein** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Wenn Sie den Veröffentlichungskompatibilitätsgrad erhöhen, können alle vorhandenen Abonnements auf Servern, auf denen eine Version vor diesem Kompatibilitätsgrad ausgeführt wird, nicht mehr synchronisiert werden.  
  
> [!NOTE]  
>  Da der Kompatibilitätsgrad Auswirkungen auf andere Veröffentlichungseigenschaften und darauf hat, welche Artikeleigenschaften gültig sind, dürfen Sie den Kompatibilitätsgrad nicht gleichzeitig mit anderen Eigenschaften im Dialogfeld ändern. Die Momentaufnahme für die Veröffentlichung sollte nach dem Ändern der Eigenschaften neu generiert werden.  
  
#### So legen Sie den Veröffentlichungskompatibilitätsgrad fest  
  
-   Wählen Sie auf der Seite **Abonnementtypen** des Assistenten für neue Veröffentlichung die Abonnententypen aus, die die Veröffentlichung unterstützen soll.  
  
#### So erhöhen Sie den Veröffentlichungskompatibilitätsgrad  
  
-   Auf die **Allgemein** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** für Wählen Sie im Dialogfeld **Kompatibilitätsgrad**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Der Kompatibilitätsgrad einer Mergeveröffentlichung kann entweder programmgesteuert während der Erstellung der Veröffentlichung festgelegt oder zu einem späteren Zeitpunkt programmgesteuert geändert werden. Sie können gespeicherte Replikationsprozeduren verwenden, um diese Veröffentlichungseigenschaft festzulegen oder zu ändern.  
  
#### So legen Sie den Veröffentlichungskompatibilitätsgrad einer Mergeveröffentlichung fest  
  
1.  Führen Sie auf dem Verleger [Sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), Angeben eines Werts für **@publication_compatibility_level** die Veröffentlichung mit älteren Versionen von kompatibel machen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### So ändern Sie den Veröffentlichungskompatibilitätsgrad einer Mergeveröffentlichung  
  
1.  Führen Sie [Sp_changemergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), wobei **publication_compatibility_level-Wert** für **@property** und die entsprechenden veröffentlichungskompatibilitätsgrads für **@value**.  
  
#### So bestimmen Sie den Veröffentlichungskompatibilitätsgrad einer Mergeveröffentlichung  
  
1.  Führen Sie [Sp_helpmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), Angabe der gewünschten Veröffentlichung.  
  
2.  Suchen Sie den Kompatibilitätsgrad der Veröffentlichung in der **Backward_comp_level** Spalte im Resultset.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird eine Mergeveröffentlichung erstellt und der Veröffentlichungskompatibilitätsgrad festgelegt.  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 In diesem Beispiel wird der Veröffentlichungskompatibilitätsgrad einer Mergeveröffentlichung geändert.  
  
> [!NOTE]  
>  Wenn in der Veröffentlichung Funktionen verwendet werden, die einen bestimmten Kompatibilitätsgrad erfordern, darf der Veröffentlichungskompatibilitätsgrad möglicherweise nicht geändert werden. Weitere Informationen finden Sie unter [Abwärtskompatibilität von Replikationen](../../../relational-databases/replication/replication-backward-compatibility.md).  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 In diesem Beispiel wird der aktuelle Veröffentlichungskompatibilitätsgrad einer Mergeveröffentlichung zurückgegeben.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  