---
title: Sp_syspolicy_update_policy_category (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_update_policy_category_TSQL
- sp_syspolicy_update_policy_category
dev_langs: TSQL
helpviewer_keywords: sp_syspolicy_update_policy_category
ms.assetid: 6b6413c2-7a3b-4eff-91d9-5db2011869d6
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3146a592bc55ee121de11f3a1c24102fcc10022
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spsyspolicyupdatepolicycategory-transact-sql"></a>sp_syspolicy_update_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert, ob eine Richtlinienkategorie Datenbankabonnements beauftragen kann. Wenn das Abonnement beauftragt wird, gilt die Richtlinienkategorie für alle Datenbanken.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syspolicy_update_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
    , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name=** ] **"***Namen***"**  
 Ist der Name der Richtlinienkategorie. *Namen* ist **Sysname**, und muss angegeben werden, wenn *Policy_category_id* ist NULL.  
  
 [  **@policy_category_id=** ] *Policy_category_id*  
 Der Bezeichner für die Richtlinienkategorie. *Policy_category_id* ist **Int**, und muss angegeben werden, wenn *Namen* ist NULL.  
  
 [  **@mandate_database_subscriptions=** ] *Mandate_database_subscriptions*  
 Bestimmt, ob das Datenbankabonnement für die Richtlinienkategorie beauftragt wird. *Mandate_database_subscriptions* ist ein **Bit** -Wert, mit dem Standardwert NULL. Sie können einen der folgenden Werte verwenden:  
  
-   0 = Nicht beauftragt  
  
-   1 = Beauftragt  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen sp_syspolicy_update_policy_category im Kontext der Systemdatenbank msdb ausführen.  
  
 Geben Sie einen Wert für beide *Namen* oder *Policy_category_id*. Keiner der Werte darf NULL sein. Um diese Werte abzurufen, fragen Sie die Systemsicht msdb.dbo.syspolicy_policy_categories ab.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Mögliche Erweiterung der Anmeldeinformationen: Benutzer mit der Rolle PolicyAdministratorRole können Servertrigger erstellen und die Ausführung von Richtlinien planen. Dies kann sich auf die Arbeitsweise der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz auswirken. Ein Benutzer mit der Rolle PolicyAdministratorRole kann beispielsweise eine Richtlinie erstellen, durch die das Erstellen der meisten Objekte in [!INCLUDE[ssDE](../../includes/ssde-md.md)] verhindert wird. Aufgrund dieser möglichen Erweiterung der Anmeldeinformationen, sollte die PolicyAdministratorRole-Rolle gewährt werden nur für Benutzer, die hinsichtlich der Kontrolle der Konfigurations der vertrauenswürdig sind die [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Kategorie "Finance" aktualisiert, um Datenbankabonnements zu beauftragen.  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category @name = N'Finance'  
, @mandate_database_subscriptions = 1;  
  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Richtlinienbasierte Verwaltung gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Sp_syspolicy_add_policy_category &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [Sp_syspolicy_delete_policy_category &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)   
 [Sp_syspolicy_rename_policy_category &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-category-transact-sql.md)  
  
  
