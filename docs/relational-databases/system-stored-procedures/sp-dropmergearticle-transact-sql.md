---
title: Sp_dropmergearticle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords: sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 902a28f31abdc9dd501c6352acd4b2bee4042fd0
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="spdropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen Artikel aus einer Mergeveröffentlichung. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, aus der ein Artikel gelöscht werden soll. *Veröffentlichung*ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name des Artikels, der aus der angegebenen Veröffentlichung gelöscht werden soll. *Artikel*ist **Sysname**, hat keinen Standardwert. Wenn **alle**, werden alle vorhandenen Artikel in der angegebenen Mergeveröffentlichung entfernt. Auch wenn *Artikel* ist **alle**, die Veröffentlichung trotzdem muss gelöscht werden separat aus dem Artikel.  
  
 [  **@ignore_distributor=**] *Ignore_distributor*  
 Gibt an, ob diese gespeicherte Prozedur ausgeführt wird, ohne eine Verbindung mit dem Verteiler herzustellen. *Ignore_distributor* ist **Bit**, hat den Standardwert **0**.  
  
 [  **@reserved=**] *reservierte*  
 Ist für die zukünftige Verwendung reserviert. *reservierte* ist **nvarchar(20)**, hat den Standardwert NULL.  
  
 [  **@force_invalidate_snapshot=**] *Force_invalidate_snapshot*  
 Aktiviert oder deaktiviert die Möglichkeit, eine Momentaufnahme für ungültig zu erklären. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Mergeartikel bewirken nicht, die Momentaufnahme ungültig zu sein.  
  
 **1** bedeutet, dass am Mergeartikel Änderungen kann dazu führen, dass die Momentaufnahme ungültig, wenn dies zutrifft, wird ein Wert von **1** Berechtigung für das Auftreten der neuen Momentaufnahme erteilt.  
  
 [  **@force_reinit_subscription =** ] *Force_reinit_subscription*  
 Bestätigt, dass durch das Löschen des Artikels eine erneute Initialisierung der vorhandenen Abonnements erforderlich wird. *Force_reinit_subscription* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass die eigentliche Löschen des Artikels nicht das Abonnement erneut initialisiert werden kann.  
  
 **1** bedeutet, dass dieser Artikel erneute Initialisierung vorhandener Abonnements bewirken löschen und Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
 [  **@ignore_merge_metadata=** ] *Ignore_merge_metadata*  
 Nur interne Verwendung.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropmergearticle** wird bei der Mergereplikation verwendet. Weitere Informationen zum Löschen von Artikeln finden Sie unter [hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 Ausführen von **Sp_dropmergearticle** zum Löschen eines Artikels aus einer Veröffentlichung entfernt jedoch nicht das Objekt aus der Veröffentlichungsdatenbank noch das zugehörige Objekt aus der Abonnementdatenbank. Verwenden Sie `DROP <object>`, um diese Objekte bei Bedarf manuell zu entfernen.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_dropmergearticle**.  
  
## <a name="example"></a>Beispiel  
  
```sql  
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
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen eines Artikels](../../relational-databases/replication/publish/delete-an-article.md)   
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Sp_addmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
