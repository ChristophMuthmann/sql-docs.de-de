---
title: Sp_articleview (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 165f494482aaac169eef7137bd0b45c0fa8b55d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt die Sicht für die Definition des veröffentlichten Artikels, wenn eine Tabelle vertikal oder horizontal gefiltert wird. Diese Sicht wird als gefilterte Quelle des Schemas und der Daten für die Zieltabellen verwendet. Mit dieser gespeicherten Prozedur können nur nicht abonnierte Artikel geändert werden. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, die den Artikel enthält. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@article=**] **"***Artikel***"**  
 Der Name des Artikels. *Artikel* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@view_name=**] **"***View_name***"**  
 Der Name der Sicht, die den veröffentlichten Artikel definiert. *View_name* ist **nvarchar(386)**, hat den Standardwert NULL.  
  
 [  **@filter_clause=**] **"***Filter_clause***"**  
 Eine Einschränkungsklausel (WHERE), die einen horizontalen Filter definiert. Wenn Sie die Einschränkungsklausel eingeben, lassen Sie das Schlüsselwort WHERE weg. *Filter_clause* ist **Ntext**, hat den Standardwert NULL.  
  
 [  **@change_active =** ] *Change_active*  
 Ermöglicht das Ändern der Spalten in Veröffentlichungen, für die Abonnements vorhanden sind. *Change_active* ist ein **Int**, hat den Standardwert **0**. Wenn **0**, Spalten nicht geändert werden. Wenn **1**, Ansichten erstellt oder für aktive Artikel, die Abonnements wurden neu erstellt werden können.  
  
 [  **@force_invalidate_snapshot =** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Artikel bewirken nicht, die Momentaufnahme ungültig wird. Wenn die gespeicherte Prozedur erkennt, dass die Änderungen eine neue Momentaufnahme erfordern, tritt ein Fehler auf und es werden keine Änderungen vorgenommen.  
  
 **1** gibt an, dass Änderungen am Artikel kann dazu führen, dass die Momentaufnahme ungültig wird, und wenn es sind Abonnements vorhanden, die eine neue Momentaufnahme erfordern die Berechtigung erteilt, für die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme zu generieren.  
  
 [  **@force_reinit_subscription =]** *Force_reinit_subscription*  
 Bestätigt, dass die von dieser gespeicherten Prozedur ausgeführte Aktion die erneute Initialisierung vorhandener Abonnements erfordern kann. *Force_reinit_subscription* ist ein **Bit** hat den Standardwert **0**.  
  
 **0** gibt an, dass Änderungen am Artikel nicht das Abonnement erneut initialisiert werden können. Wenn die gespeicherte Prozedur erkennt, dass die Änderung die erneute Initialisierung von Abonnements erfordert, wird ein Fehler auftritt und keine Änderungen vorgenommen werden.  
  
 **1** gibt an, dass Änderungen am Artikel bewirkt, dass vorhandene Abonnements erneut initialisiert werden, und die Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
 [  **@publisher** =] **"***Publisher***"**  
 Gibt einen nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
 [  **@refreshsynctranprocs**  =] *Refreshsynctranprocs*  
 Gibt an, ob die gespeicherten Prozeduren, die zum Synchronisieren der Replikation verwendet werden, automatisch neu erstellt werden. *Refreshsynctranprocs* ist **Bit**, hat den Standardwert 1.  
  
 **1** bedeutet, dass die gespeicherten Prozeduren neu erstellt werden.  
  
 **0** bedeutet, dass die gespeicherten Prozeduren nicht erneut erstellt werden.  
  
 [  **@internal** =] *interne*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_articleview** erstellt die Sicht, die Definition des veröffentlichten Artikels und fügt die ID der Sicht in der **Sync_objid** Spalte die [Sysarticles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) Tabelle, und fügt den Text der Einschränkungsklausel in die **Filter_clause** Spalte. Wenn alle Spalten repliziert werden, und es ist keine **Filter_clause**, **Sync_objid** in die [Sysarticles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) Tabelle festgelegt ist, um die ID der Basistabelle und die Verwendung von **Sp_articleview** ist nicht erforderlich.  
  
 So veröffentlichen Sie eine vertikal gefilterte Tabelle (d. h. zum Filtern von Spalten) führen Sie zuerst **Sp_addarticle** ohne *Sync_object* -Parameter aus, [Sp_articlecolumn &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) einmal für jede Spalte an (zum Definieren des vertikalen Filters) repliziert werden, und führen Sie **Sp_articleview** auf die Ansicht zu erstellen, die den veröffentlichten Artikel definiert.  
  
 So veröffentlichen Sie eine horizontal gefilterte Tabelle (d. h. zum Filtern von Zeilen), führen Sie [Sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) ohne *Filter* Parameter. Führen Sie [Sp_articlefilter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), dabei alle Parameter einschließlich *Filter_clause*. Führen Sie **Sp_articleview**, dabei alle Parameter einschließlich eines identischen *Filter_clause*.  
  
 Um eine vertikal und horizontal partitionierte Tabelle zu veröffentlichen, führen Sie [Sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) ohne *Sync_object* oder *Filter* Parameter. Führen Sie [Sp_articlecolumn &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) für jede zu replizierende Spalte einmal aus, und führen Sie [Sp_articlefilter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) und **Sp_articleview**.  
  
 Wenn der Artikel bereits eine Sicht enthält, die den veröffentlichten Artikel definiert **Sp_articleview** löscht die vorhandene Sicht und erstellt automatisch eine neue. Wenn die Sicht manuell erstellt wurde (**Typ** in [Sysarticles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) ist **5**), die vorhandene Sicht nicht gelöscht.  
  
 Wenn Sie erstellen eine benutzerdefinierte gespeicherte Filterprozedur und eine Sicht, die den veröffentlichten Artikel manuell definiert werden, werden nicht ausgeführt **Sp_articleview**. Geben Sie diese als stattdessen die *Filter* und *Sync_object* Parameter [Sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), zusammen mit dem entsprechenden *Typ* Wert.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_articleview**.  
  
## <a name="see-also"></a>Siehe auch  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definieren und Ändern eines statischen Zeilenfilters](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [Sp_addarticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
