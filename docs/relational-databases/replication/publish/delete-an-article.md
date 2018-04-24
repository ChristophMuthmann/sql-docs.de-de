---
title: Löschen eines Artikels | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04461784ec6522536e0b7fba2b15b242796c0cd0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="delete-an-article"></a>Löschen eines Artikels
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie ein Artikel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) gelöscht wird. Informationen über die Bedingungen, unter denen Artikel gelöscht werden können, und darüber, ob das Löschen eines Artikels eine neue Momentaufnahme oder die erneute Initialisierung der Abonnements erforderlich macht, finden Sie unter [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **In diesem Thema**  
  
-   **So löschen Sie einen Artikel mit:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Artikel können programmgesteuert mit gespeicherten Replikationsprozeduren gelöscht werden. Die verwendeten gespeicherten Prozeduren hängen vom Typ der Veröffentlichung ab, zu der der Artikel gehört.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>So löschen Sie einen Artikel aus einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie [sp_droparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) aus, um einen durch **@article** angegebenen Artikel von der durch **@publication** angegebenen Veröffentlichung zu löschen. Geben Sie den Wert **1** für **@force_invalidate_snapshot**.  
  
2.  (Optional) Um das veröffentlichte Objekt vollständig aus der Veröffentlichungsdatenbank zu löschen, führen Sie den Befehl `DROP <objectname>` auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>So löschen Sie einen Artikel aus einer Mergeveröffentlichung  
  
1.  Führen Sie [sp_dropmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) aus, um einen durch **@article** angegebenen Artikel von der durch **@publication** angegebenen Veröffentlichung zu löschen. Geben Sie dafür, falls notwendig, den Wert **1** für **@force_invalidate_snapshot** und den Wert **1** für **@force_reinit_subscription**.  
  
2.  (Optional) Um das veröffentlichte Objekt vollständig aus der Veröffentlichungsdatenbank zu löschen, führen Sie den Befehl `DROP <objectname>` auf dem Verleger für die Veröffentlichungsdatenbank aus.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird ein Artikel aus einer Transaktionsveröffentlichung gelöscht. Da durch diese Änderung die vorhandene Momentaufnahme ungültig wird, wird der Wert **1** für den Parameter **@force_invalidate_snapshot** angegeben.  
  
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
  
 Im folgenden Beispiel werden zwei Artikel aus einer Mergeveröffentlichung gelöscht. Da durch diese Änderungen die vorhandene Momentaufnahme ungültig wird, wird der Wert **1** für den Parameter **@force_invalidate_snapshot** angegeben.  
  
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
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>So löschen Sie einen Artikel, der zu einer Momentaufnahme- oder Transaktionsveröffentlichung gehört  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.TransArticle> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> fest.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft, um festzustellen, ob der Artikel vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> -Methode auf.  
  
7.  Trennen Sie alle Verbindungen.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>So löschen Sie einen Artikel, der zu einer Mergeveröffentlichung gehört  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger, indem Sie die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Klasse verwenden.  
  
2.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeArticle> -Klasse.  
  
3.  Legen Sie die Eigenschaften <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>und <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> fest.  
  
4.  Legen Sie die Verbindung aus Schritt 1 für die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> -Eigenschaft fest.  
  
5.  Überprüfen Sie die <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> -Eigenschaft, um festzustellen, ob der Artikel vorhanden ist. Wenn der Wert dieser Eigenschaft **false**lautet, wurden entweder die Artikeleigenschaften in Schritt 3 falsch definiert, oder der Artikel ist nicht vorhanden.  
  
6.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> -Methode auf.  
  
7.  Trennen Sie alle Verbindungen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
