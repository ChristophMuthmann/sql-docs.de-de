---
title: Sp_syspolicy_purge_health_state (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_syspolicy_purge_health_state_TSQL
- sp_syspolicy_purge_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_purge_health_state
ms.assetid: 4ba4aa91-4c19-41c7-b70d-5fd9d0e89a5e
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b8372d9ad0774479bac1f5572638ffd6eb8894e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsyspolicypurgehealthstate-transact-sql"></a>sp_syspolicy_purge_health_state (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Löscht die Richtlinienzustandsstatus in der richtlinienbasierten Verwaltung. Richtlinienzustandsstatus sind visuelle Indikatoren (ein Bildlaufsymbol mit einem roten "X") innerhalb des Objekt-Explorers, mit denen Sie bestimmen können, für welche Knoten die Richtlinienauswertung fehlerhaft ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syspolicy_purge_health_state [ @target_tree_root_with_id = ] 'target_tree_root_with_id'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@target_tree_root_with_id =** ] **"***Target_tree_root_with_id***"**  
 Stellt den Knoten im Objekt-Explorer dar, an dem Sie den Status des Zustands löschen möchten. hat den Wert. *Target_tree_root_with_id* ist **nvarchar(400)**, hat den Standardwert NULL.  
  
 Sie können in der Spalte target_query_expression_with_id der Systemsicht msdb.dbo.syspolicy_system_health_state Werte angeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen sp_syspolicy_purge_health_state im Kontext der Systemdatenbank msdb ausführen.  
  
 Wenn Sie diese gespeicherte Prozedur ganz ohne Parameter ausführen, wird der Systemzustandsstatus für alle Knoten im Objekt-Explorer gelöscht.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Mögliche Erweiterung der Anmeldeinformationen: Benutzer mit der Rolle PolicyAdministratorRole können Servertrigger erstellen und die Ausführung von Richtlinien planen. Dies kann sich auf die Arbeitsweise der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz auswirken. Ein Benutzer mit der Rolle PolicyAdministratorRole kann beispielsweise eine Richtlinie erstellen, durch die das Erstellen der meisten Objekte in [!INCLUDE[ssDE](../../includes/ssde-md.md)] verhindert wird. Aufgrund dieser möglichen Erweiterung der Anmeldeinformationen, sollte die PolicyAdministratorRole-Rolle gewährt werden nur für Benutzer, die hinsichtlich der Kontrolle der Konfigurations der vertrauenswürdig sind die [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die verschiedenen Zustandsstatus für einen bestimmten Knoten im Objekt-Explorer gelöscht.  
  
```  
EXEC msdb.dbo.sp_syspolicy_purge_health_state @target_tree_root_with_id = 'Server/Database[@ID=7]';  
  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren Richtlinie der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
