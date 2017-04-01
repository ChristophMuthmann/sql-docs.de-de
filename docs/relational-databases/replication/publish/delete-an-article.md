---
title: "L&#246;schen eines Artikels | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Artikel [SQL Server-Replikation], löschen"
  - "sp_droparticle"
  - "sp_dropmergearticle"
  - "Löschen von Artikeln"
  - "Entfernen von Artikeln"
  - "Löschung von Artikeln"
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# L&#246;schen eines Artikels
  In diesem Thema wird beschrieben, wie ein Artikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) gelöscht wird. Weitere Informationen über die Umstände, unter denen Artikel gelöscht werden können und ob Löschen eines Artikels eine neue Momentaufnahme oder die erneute Initialisierung der Abonnements erforderlich ist, finden Sie unter [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **In diesem Thema**  
  
-   **So löschen Sie einen Artikel mit:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Artikel können programmgesteuert mit gespeicherten Replikationsprozeduren gelöscht werden. Die verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, zu der der Artikel gehört.  
  
#### So löschen Sie einen Artikel aus einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie [Sp_droparticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) So löschen Sie einen Artikel, angegeben durch **@article**, aus einer Veröffentlichung, die durch angegebene **@publication**. Geben Sie den Wert **1** für **@force_invalidate_snapshot**.  
  
2.  (Optional) Um das veröffentlichte Objekt vollständig aus der Veröffentlichungsdatenbank zu löschen, führen Sie den Befehl `DROP <objectname>` auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
#### So löschen Sie einen Artikel aus einer Mergeveröffentlichung  
  
1.  Führen Sie [Sp_dropmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) So löschen Sie einen Artikel, angegeben durch **@article**, aus einer Veröffentlichung, die durch angegebene **@publication**. Falls erforderlich, geben Sie den Wert **1** für **@force_invalidate_snapshot** und einem Wert von **1** für **@force_reinit_subscription**.  
  
2.  (Optional) Um das veröffentlichte Objekt vollständig aus der Veröffentlichungsdatenbank zu löschen, führen Sie den Befehl `DROP <objectname>` auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird ein Artikel aus einer Transaktionsveröffentlichung gelöscht. Da diese Änderung die vorhandene Momentaufnahme, der Wert ungültig **1** wird angegeben, für die **@force_invalidate_snapshot** Parameter.  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 Im folgenden Beispiel werden zwei Artikel aus einer Mergeveröffentlichung gelöscht. Da diese Änderungen die vorhandene Momentaufnahme, der Wert ungültig **1** wird angegeben, für die **@force_invalidate_snapshot** Parameter.  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Artikel mithilfe von Replikationsverwaltungsobjekten (RMO) programmgesteuert löschen. Welche RMO-Klassen Sie zum Löschen eines Artikels verwenden, hängt vom Typ der Veröffentlichung ab, zu der der Artikel gehört.  
  
#### So löschen Sie einen Artikel, der zu einer Momentaufnahme- oder Transaktionsveröffentlichung gehört  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransArticle> Klasse.  
  
3.  Legen Sie den <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> Eigenschaft zu überprüfen, ob der Artikel vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> Methode.  
  
7.  Trennen Sie alle Verbindungen.  
  
#### So löschen Sie einen Artikel, der zu einer Mergeveröffentlichung gehört  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> Klasse.  
  
3.  Legen Sie den <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Eigenschaften.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> Eigenschaft zu überprüfen, ob der Artikel vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> Methode.  
  
7.  Trennen Sie alle Verbindungen.  
  
## Siehe auch  
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  