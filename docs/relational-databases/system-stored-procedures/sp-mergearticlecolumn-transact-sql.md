---
title: Sp_mergearticlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 083d6d27d9417a76f9cafc1c3726e3f7c10df6d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spmergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt eine vertikale Partitionierung einer Mergeveröffentlichung durch. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication =**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article =**] **"***Artikel***"**  
 Der Name des Artikels in der Veröffentlichung. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@column =**] **"***Spalte***"**  
 Identifiziert die Spalten, für die die vertikale Partition erstellt werden soll. *Spalte* ist **Sysname**, hat den Standardwert NULL. Bei den Werten NULL und `@operation = N'add'` werden dem Artikel standardmäßig alle Spalten in der Quelltabelle hinzugefügt. *Spalte* darf nicht NULL sein, wenn *Vorgang* festgelegt ist, um **löschen**. Führen Sie zum Ausschließen von Spalten aus einem Artikel **Sp_mergearticlecolumn** , und geben Sie *Spalte* und `@operation = N'drop'` für jede Spalte, die entfernt werden aus dem angegebenen *Artikel*.  
  
 [  **@operation =**] **"***Vorgang***"**  
 Der Replikationsstatus. *Vorgang* ist **nvarchar(4)**, hat den Standardwert ADD. **Hinzufügen** markiert die Spalte für die Replikation. **Drop** wird die Spalte gelöscht.  
  
 [  **@schema_replication=**] **"***Schema_replication***"**  
 Gibt an, dass eine Schemaänderung weitergegeben wird, wenn der Merge-Agent ausgeführt wird. *Schema_replication* ist **nvarchar(5)**, hat den Standardwert "false".  
  
> [!NOTE]  
>  Nur **"false"** direkteinplanung *Schema_replication*.  
  
 [  **@force_invalidate_snapshot =** ] *Force_invalidate_snapshot*  
 Aktiviert oder deaktiviert die Möglichkeit, eine Momentaufnahme für ungültig zu erklären. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Mergeartikel nicht die Momentaufnahme ungültig werden.  
  
 **1** gibt an, dass Änderungen am Mergeartikel bewirken, dass die Momentaufnahme ungültig ist, wird möglicherweise Wenn dies zutrifft, wird ein Wert von **1** Berechtigung für das Auftreten der neuen Momentaufnahme erteilt.  
  
 [  **@force_reinit_subscription =]***Force_reinit_subscription*  
 Aktiviert oder deaktiviert die Möglichkeit, das Abonnement erneut zu initialisieren. *Force_reinit_subscription* ist vom Datentyp bit mit dem Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Mergeartikel nicht werden dazu, dass das Abonnement erneut initialisiert werden.  
  
 **1** gibt an, dass Änderungen am Mergeartikel bewirken, dass das Abonnement erneut initialisiert werden, möglicherweise Wenn dies zutrifft, wird ein Wert von **1** Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_mergearticlecolumn** wird bei der Mergereplikation verwendet.  
  
 Eine Identitätsspalte kann nicht aus dem Artikel gelöscht werden, wenn die automatische Identitätsbereichsverwaltung verwendet wird. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Wenn eine Anwendung eine neue vertikale Partition festlegt, nachdem die Anfangsmomentaufnahme erstellt wurde, muss eine neue Momentaufnahme generiert und auf jedes Abonnement erneut angewendet werden. Momentaufnahmen werden angewendet, wenn die nächste geplante Momentaufnahme und der Verteilungs- oder Merge-Agent ausgeführt werden.  
  
 Falls die Zeilennachverfolgung zur Konflikterkennung verwendet wird (Standardeinstellung), kann die Basistabelle maximal 1.024 Spalten enthalten. Die Spalten müssen jedoch im Artikel gefiltert werden, sodass maximal 246 Spalten veröffentlicht werden. Wenn Spaltennachverfolgung verwendet wird, kann die Basistabelle maximal 246 Spalten enthalten.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_mergearticlecolumn**.  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
