---
title: Syspolicy_policy_category_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fac13c1a1da914c658f9c7b6a01bfa5124810ed
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt für jedes Abonnement der richtlinienbasierten Verwaltung in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Zeile an. Jede Zeile beschreibt ein Paar aus Ziel und Richtlinienkategorie. In der folgenden Tabelle werden die Spalten in der syspolicy_policy_group_subscriptions-Sicht beschrieben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|Bezeichner des Datensatzes.|  
|target_type|**sysname**|Typ des Datenbankobjekts, das Ziel des Abonnements ist.|  
|target_object|**sysname**|Name des Zielobjekts|  
|policy_category_id|**int**|ID der Richtlinienkategorie, die auf das Ziel angewendet wird.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Sicht zeigt die Ziele an, die für Richtlinienkategorien abonniert werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Sichten der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
