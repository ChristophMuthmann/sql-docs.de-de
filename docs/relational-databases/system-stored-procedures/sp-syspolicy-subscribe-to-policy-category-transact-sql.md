---
title: Sp_syspolicy_subscribe_to_policy_category (Transact-SQL) | Microsoft Docs
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
- sp_syspolicy_subscribe_to_policy_category
- sp_syspolicy_subscribe_to_policy_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_subscribe_to_policy_category
ms.assetid: de88cc49-bcc8-4dc6-8e59-ad85cfbfb2fb
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2590dd0cfcb797f289580d4f7c5456c4c3fee845
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsyspolicysubscribetopolicycategory-transact-sql"></a>sp_syspolicy_subscribe_to_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt ein richtlinienkategorieabonnement für die angegebene Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syspolicy_subscribe_to_policy_category [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@policy_category=** ] **'***policy_category***'**  
 Der Name der Richtlinienkategorie, die die Datenbank abonnieren soll. *Policy_category* ist **Sysname**, und es ist erforderlich.  
  
 Zum Abrufen von Werten für *Policy_category*, Fragen Sie die Systemsicht syspolicy_policy_categories ab.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen sp_syspolicy_subscribe_to_policy_category im Kontext der Datenbank ausführen, in der Sie ein Richtlinienkategorieabonnement hinzufügen möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle "db_owner".  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird für die angegebene Datenbank ein Abonnement der Richtlinienkategorie "Finance" hinzugefügt.  
  
```  
USE <database_name>;  
  
EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren Richtlinie der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
