---
title: Syspolicy_policies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- syspolicy_policies_TSQL
- syspolicy_policies
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policies view
ms.assetid: aecf35bb-187e-4f80-870f-48081b88974e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e70f2cd4464e37933acb08624eaf07ed9c4d6135
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspolicypolicies-transact-sql"></a>syspolicy_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt eine Zeile für jede Richtlinie der richtlinienbasierten Verwaltung in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Syspolicy_policies gehört zum Dbo-Schema in der Msdb-Datenbank. In der folgenden Tabelle werden die Spalten in der syspolicy_policies-Sicht beschrieben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|policy_id|**int**|Bezeichner der Richtlinie.|  
|name|**sysname**|Name der Richtlinie.|  
|condition_id|**int**|ID der Bedingung, die durch diese Richtlinie erzwungen oder getestet wird.|  
|root_condition_id|**int**|Nur zur internen Verwendung.|  
|date_created|**datetime**|Datum und Uhrzeit der Erstellung der Richtlinie.|  
|execution_mode|**int**|Auswertungsmodus für die Richtlinie. Mögliche Werte sind wie folgt aus:<br /><br /> 0 = Bedarfsgesteuert<br /><br /> Dieser Modus wertet die Richtlinie aus, wenn sie vom Benutzer direkt angegeben wird.<br /><br /> 1 = Bei Änderung: Verhindern<br /><br /> Dieser automatisierte Modus verwendet DDL-Trigger, um Richtlinienverstöße zu verhindern.<br /><br /> 2 = Bei Änderung: Nur protokollieren<br /><br /> Dieser automatisierte Modus verwendet die Ereignisbenachrichtigung, um eine Richtlinie dann auszuwerten, wenn eine relevante Änderung auftritt. Die Richtlinienverstöße werden protokolliert.<br /><br /> 4 = Nach Zeitplan<br /><br /> Dieser automatisierte Modus verwendet einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentauftrag, um eine Richtlinie in regelmäßigen Abständen auszuwerten. In diesem Modus werden Richtlinienverstöße protokolliert.<br /><br /> Hinweis: Der Wert 3 ist kein mögliche Wert.|  
|policy_category|**int**|ID der Richtlinienkategorie der richtlinienbasierten Verwaltung, zu der diese Richtlinie gehört. Ist NULL, wenn sie sich in der Standardrichtliniengruppe befindet.|  
|schedule_uid|**uniqueidentifier**|Enthält die ID des Zeitplans, wenn execution_mode den Wert Nach Zeitplan aufweist. Ist andernfalls NULL.|  
|description|**nvarchar(max)**|Beschreibung der Richtlinie. Die Beschreibungsspalte ist optional und kann NULL sein.|  
|help_text|**nvarchar(4000)**|Der Linktext, der zu help_link gehört.|  
|help_link|**nvarchar(2083)**|Der zusätzliche Hilfelink, der der Richtlinie vom Richtlinienersteller zugewiesen wird.|  
|object_set_id|**int**|ID des Objektsatzes, den die Richtlinie auswertet.|  
|is_enabled|**bit**|Gibt an, ob die Richtlinie zurzeit aktiviert (1) oder deaktiviert (0) ist.|  
|job_id|**uniqueidentifier**|Enthält die ID des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Auftrags, der die Richtlinie ausführt, wenn execution_mode den Wert Nach Zeitplan aufweist.|  
|created_by|**sysname**|Anmeldung, die die Richtlinie erstellt hat.|  
|modified_by|**sysname**|Anmeldung, die die Richtlinie zuletzt geändert hat. Ist NULL, wenn nie geändert.|  
|date_modified|**datetime**|Datum und Uhrzeit der Erstellung der Richtlinie. Ist NULL, wenn nie geändert.|  
  
## <a name="remarks"></a>Hinweise  
 Bei der Problembehandlung von Richtlinie der richtlinienbasierten Verwaltung Fragen Sie die [Syspolicy_conditions](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md) Ansicht, um zu bestimmen, ob die Richtlinie aktiviert ist. Diese Sicht zeigt darüber hinaus an, wer die Richtlinie erstellt oder zuletzt geändert hat.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Sichten der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
