---
title: dbo. slo_assignment_history (Azure SQL-Datenbank) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
- slo_assignment_history_TSQL
- dbo.slo_assignment_history_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
ms.assetid: 048a6fb5-2fc2-4d12-a436-4c53ecd413f3
caps.latest.revision: "9"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61bf1f0541df9085235dc00072624e1e91425cc5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="dbosloassignmenthistory-azure-sql-database"></a>dbo.slo_assignment_history (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **Dies gilt nur für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
>   
>  Diese Funktion befindet sich in einem Vorschauzustand. Erstellen Sie keine Abhängigkeit von der spezifischen Implementierung dieser Funktion, da die Funktion in zukünftigen Versionen ggf. geändert oder entfernt werden kann.  
  
 Gibt den Verlauf der Datenbank-SLO-Zuweisungen im Server einschließlich folgender Informationen zurück:  
  
-   Der Verlauf der Datenbank-SLO-Zuweisungen im Server.  
  
-   Die Start-und Beendigungszeit jeder Datenbank-SLO-Änderungsanforderung.  
  
-   SLO-Zuweisungsfehler, die in der error_code-Spalte und error_desc-Spalte aufgezeichnet werden.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|Der Name der Datenbank.|  
|database_id|**int**|Die ID der Datenbank.|  
|create_date|**DateTimeOffset(7)**|Das Datum der Datenbankerstellung.|  
|service_objective_name|**sysname**|Der Name des Servicelevelziels (SLO, Service Level Objective).|  
|service_objective_id|**uniqueidentifier**|Die ID des SLOs.|  
|operation_id|**uniqueidentifier**|ID des Vorgangs.|  
|operation_start_time|**DateTimeOffset(7)**|Die Startzeit der Datenbank-SLO-Änderungsanforderung.|  
|operation_end_time|**DateTimeOffset(7)**|Die Beendigungszeit der Datenbank-SLO-Änderungsanforderung.|  
|error_code|**int**|Der Fehlercode der Datenbank-SLO-Änderungsanforderung.|  
|error_desc|**nvarchar**|Die Beschreibung des Fehlers in der Datenbank-SLO-Änderungsanforderung.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Verlauf der SLO-Zuweisungen für eine bestimmte Datenbank zurückgegeben.  
  
```  
SELECT *  
FROM dbo.slo_assignment_history   
WHERE database_name = '<DB NAME>’   
ORDER BY operation_start_time DESC;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Premiumdatenbanken](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
