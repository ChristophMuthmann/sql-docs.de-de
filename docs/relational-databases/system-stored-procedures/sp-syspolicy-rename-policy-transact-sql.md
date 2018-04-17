---
title: Sp_syspolicy_rename_policy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_rename_policy_TSQL
- sp_syspolicy_rename_policy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_rename_policy
ms.assetid: ce2b07f5-23b1-4f49-8e7b-c18cf3f3d45b
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83e70da7cf1ee976206052e33cf2a9708b903e36
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spsyspolicyrenamepolicy-transact-sql"></a>sp_syspolicy_rename_policy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Benennt in der richtlinienbasierten Verwaltung eine vorhandene Richtlinie um.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syspolicy_rename_policy { [ @name = ] 'name' | [ @policy_id = ] policy_id }  
    , [ @new_name = ] 'new_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@name=** ] **'***name***'**  
 Der Name der Richtlinie, die Sie umbenennen möchten. *Namen* ist **Sysname**, und muss angegeben werden, wenn *Policy_id* ist NULL.  
  
 [ **@policy_id=** ] *policy_id*  
 Der Bezeichner für die Richtlinie, die Sie umbenennen möchten. *Policy_id* ist **Int**, und muss angegeben werden, wenn *Namen* ist NULL.  
  
 [  **@new_name=** ] **"***New_name***"**  
 Ist der neue Name für die Richtlinie. *New_name* ist **Sysname**, und es ist erforderlich. Darf nicht NULL und keine leere Zeichenfolge sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen sp_syspolicy_rename_policy im Kontext der Systemdatenbank msdb ausführen.  
  
 Geben Sie einen Wert für beide *Namen* oder *Policy_id*. Keiner der Werte darf NULL sein. Um diese Werte abzurufen, fragen Sie die Systemsicht msdb.dbo.syspolicy_policies ab.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Mögliche Erweiterung der Anmeldeinformationen: Benutzer mit der Rolle PolicyAdministratorRole können Servertrigger erstellen und die Ausführung von Richtlinien planen. Dies kann sich auf die Arbeitsweise der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz auswirken. Ein Benutzer mit der Rolle PolicyAdministratorRole kann beispielsweise eine Richtlinie erstellen, durch die das Erstellen der meisten Objekte in [!INCLUDE[ssDE](../../includes/ssde-md.md)] verhindert wird. Aufgrund dieser möglichen Erweiterung der Anmeldeinformationen, sollte die PolicyAdministratorRole-Rolle gewährt werden nur für Benutzer, die hinsichtlich der Kontrolle der Konfigurations der vertrauenswürdig sind die [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Richtlinie "Test Policy 1" in "Test Policy 2" umbenannt.  
  
```  
EXEC msdb.dbo.sp_syspolicy_rename_policy @name = N'Test Policy 1'  
, @new_name = N'Test Policy 2';  
  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren Richtlinie der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
