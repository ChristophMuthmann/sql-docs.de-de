---
title: Sp_delete_maintenance_plan (Transact-SQL) | Microsoft Docs
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
- sp_delete_maintenance_plan
- sp_delete_maintenance_plan_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_maintenance_plan
ms.assetid: 6f36b63f-3d18-4d42-9469-2febb6926530
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87d9d2da47797acd2b18a8b2edb2e69e8d0af405
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spdeletemaintenanceplan-transact-sql"></a>sp_delete_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht den angegebenen Wartungsplan.  
  
> [!NOTE]  
>  Diese gespeicherte Prozedur wird mit Datenbankwartungsplänen verwendet. Diese Funktion wurde durch Wartungspläne ersetzt, die nicht diese gespeicherte Prozedur verwenden. Verwenden Sie diese Prozedur, um Datenbankwartungspläne für Installationen bereitzustellen, die von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_maintenance_plan [ @plan_id = ] 'plan_id'   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@plan_id =**] **"***" Plan_id "***"**  
 Gibt die ID des zu löschenden Wartungsplans an. *plan_id* ist vom Datentyp **uniqueidentifier**und muss eine gültige ID sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **sp_delete_maintenance_plan** muss von der **msdb** -Datenbank ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können **sp_delete_maintenance_plan**ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird der erstellte Wartungsplan mithilfe von **sp_add_maintenance_plan**gelöscht.  
  
```  
EXECUTE sp_delete_maintenance_plan 'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Datenbank-Wartungsplan gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
