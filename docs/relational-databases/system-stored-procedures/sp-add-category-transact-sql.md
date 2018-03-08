---
title: Sp_add_category (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7df42005cfd21c4030990784c7efd482c9312118
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spaddcategory-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt dem Server die angegebene Kategorie von Aufträgen, Warnungen oder Operatoren hinzu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@class =** ] **'***class***'**  
 Die Klasse der Kategorie, die hinzugefügt werden soll. *Klasse* ist **varchar(8)** hat den Standardwert des AUFTRAGS, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|JOB|Fügt eine Auftragskategorie hinzu|  
|ALERT|Fügt eine Warnungskategorie hinzu|  
|OPERATOR|Fügt eine Operatorkategorie hinzu|  
  
 [ **@type =** ] **'***type***'**  
 Der Typ der Kategorie, die hinzugefügt werden soll. *Typ* ist **varchar(12)**, hat den Standardwert des **lokale**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|LOCAL|Lokale Auftragskategorie|  
|MIT MEHREREN SERVERN|Multiserver-Auftragskategorie.|  
|Keine|Eine Kategorie für eine Klasse als JOB**.**|  
  
 [ **@name =** ] **'***name***'**  
 Der Name der Kategorie, die hinzugefügt werden soll. Der Name muss innerhalb der angegebenen Klasse eindeutig sein. *Namen* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_add_category** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_add_category**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die lokale Auftragskategorie `AdminJobs` erstellt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_delete_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo.sysjobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
