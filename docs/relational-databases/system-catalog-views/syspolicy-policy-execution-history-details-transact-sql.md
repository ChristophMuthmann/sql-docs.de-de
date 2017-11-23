---
title: Syspolicy_policy_execution_history_details (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_details
- syspolicy_policy_execution_history_details_TSQL
dev_langs: TSQL
helpviewer_keywords: syspolicy_policy_execution_history_details view
ms.assetid: 97ef6573-5e8b-4ba5-8ae0-7901e79a9683
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bb2d7ba198275e14344be70df82e59153e341bf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syspolicypolicyexecutionhistorydetails-transact-sql"></a>syspolicy_policy_execution_history_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt die folgenden Informationen an: ausgeführte Bedingungsausdrücke, Ziele der Ausdrücke, Ergebnis der einzelnen Ausführungen, Details zu eventuell aufgetretenen Fehlern. In der folgenden Tabelle werden die Spalten in der syspolicy_execution_history_details-Sicht beschrieben.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|detail_id|**bigint**|Bezeichner des Datensatzes. Jeder Datensatz stellt den Versuch dar, einen Bedingungsausdruck in einer Richtlinie auszuwerten oder zu erzwingen. Jede Bedingung hat einen Detaildatensatz für die einzelnen Ziele, wenn sie auf mehrere Ziele angewendet wird.|  
|history_id|**bigint**|Bezeichner des Verlaufsereignisses. Jedes Verlaufsereignis stellt einen Versuch dar, eine Richtlinie auszuführen. Da eine Bedingung mehrere Bedingungsausdrücke und mehrere Ziele haben kann, kann eine history_id mehrere Detaildatensätze erstellen. Verwenden Sie die History_id-Spalte, um diese Sicht zum Verknüpfen der [Syspolicy_policy_execution_history](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-transact-sql.md) anzeigen.|  
|target_query_expression|**nvarchar(max)**|Ziel der Richtlinie und syspolicy_policy_execution_history-Sicht.|  
|execution_date|**datetime**|Datum und Uhrzeit der Erstellung dieses Detaildatensatzes.|  
|result|**bit**|Erfolg oder Fehler dieses Ziels und der Auswertung des Bedingungsausdrucks:<br /><br /> 0 (Erfolg) oder 1 (Fehler)|  
|result_detail|**nvarchar(max)**|Ergebnismeldung. Nur verfügbar, wenn durch das Facet bereitgestellt.|  
|exception_message|**nvarchar(max)**|Von der Ausnahme (falls aufgetreten) generierte Meldung.|  
|exception|**nvarchar(max)**|Beschreibung der Ausnahme, falls aufgetreten.|  
  
## <a name="remarks"></a>Hinweise  
 Bei der Problembehandlung in der richtlinienbasierten Verwaltung fragen Sie in der syspolicy_policy_execution_history_details-Sicht ab, welche Kombinationen aus Ziel und Bedingungsausdruck fehlgeschlagen sind und wann sie fehlgeschlagen sind. Darüber hinaus überprüfen Sie zugehörige Fehler.  
  
 Die folgende Abfrage verbindet die `syspolicy_policy_execution_history_details` -Sicht mit den Sichten `syspolicy_policy_execution_history_details` und `syspolicy_policies` , um den Namen der Richtlinie, den Namen der Bedingung und die Details zu Fehlern anzuzeigen.  
  
```  
SELECT Pol.name AS Policy,   
Cond.name AS Condition,   
PolHistDet.target_query_expression,   
PolHistDet.execution_date,   
PolHistDet.result,   
PolHistDet.result_detail,   
PolHistDet.exception_message,   
PolHistDet.exception   
FROM msdb.dbo.syspolicy_policies AS Pol  
JOIN msdb.dbo.syspolicy_conditions AS Cond  
    ON Pol.condition_id = Cond.condition_id  
JOIN msdb.dbo.syspolicy_policy_execution_history AS PolHist  
    ON Pol.policy_id = PolHist.policy_id  
JOIN msdb.dbo.syspolicy_policy_execution_history_details AS PolHistDet  
    ON PolHist.history_id = PolHistDet.history_id  
WHERE PolHistDet.result = 0 ;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Sichten der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
