---
title: Syspolicy_system_health_state (Transact-SQL) | Microsoft Docs
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
- syspolicy_system_health_state_TSQL
- syspolicy_system_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_system_health_state view
ms.assetid: 00815106-9fe4-481d-a9e1-a256101887f4
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e546ff0c3025812239aec6dbd1f466d9fc40c560
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspolicysystemhealthstate-transact-sql"></a>syspolicy_system_health_state (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt pro Richtlinie der richtlinienbasierten Verwaltung und Zielabfrageausdruck eine Zeile an. In der syspolicy_system_health_state-Sicht können Sie den Richtlinienzustand des Servers programmgesteuert überprüfen. In der folgenden Tabelle werden die Spalten in der syspolicy_system_health_state-Sicht beschrieben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|health_state_id|**bigint**|Bezeichner des Datensatzes zum Richtlinienzustand.|  
|policy_id|**int**|Bezeichner der Richtlinie.|  
|last_run_date|**datetime**|Datum und Uhrzeit der letzten Ausführung der Richtlinie.|  
|target_query_expression_with_id|**nvarchar(400)**|Der Zielausdruck, mit Identitätsvariablen zugewiesenen Werten, der das Ziel definiert, für das die Richtlinie ausgewertet wird.|  
|target_query_expression|**nvarchar(max)**|Der Ausdruck, der das Ziel definiert, für das die Richtlinie ausgewertet wird.|  
|result|**bit**|Zustand des Ziels im Bezug auf die Richtlinie:<br /><br /> 0 = Fehler<br /><br /> 1 = Erfolg|  
  
## <a name="remarks"></a>Hinweise  
 In der Sicht syspolicy_system_health_state wird der letzte Zustand des Zielabfrageausdrucks für die einzelnen aktiven (aktivierten) Richtlinien angezeigt. Auf den [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]-Seiten Objekt-Explorer und Details zum Objekt-Explorer werden die Zustände der Richtlinien aus dieser Sicht summiert, um den kritischen Zustand anzuzeigen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Sichten der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
