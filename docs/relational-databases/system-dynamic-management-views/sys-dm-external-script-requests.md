---
title: dm_external_script_requests | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b73281b970940caced870dbf75c78946f9f559b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexternalscriptrequests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Gibt eine Zeile für jedes aktive Workerkonto zurück, das ein externes Skript ausführt.
 
  
> [!NOTE] 
>  
>  Diese dynamische Verwaltungssicht ist nur verfügbar, wenn Sie die Funktion installiert und aktiviert haben, die die Ausführung von externen Skripts unterstützt. Informationen dazu, wie dies für R-Skripts erledigt wird, finden Sie unter [Einrichten von SQL Server R-Diensten](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**Eindeutiger Bezeichner**|Die ID des Prozesses, der die externe Skriptanforderung gesendet hat. Dies entspricht dem Prozess-ID beim Empfangen von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|Sprache|**nvarchar**|Schlüsselwort, das einer unterstützten Skriptsprache entspricht. Derzeit wird nur `R` unterstützt.|  
|degree_of_parallelism|**int**|Zahl, die die Anzahl von parallelen Prozessen angibt, die erstellt wurden. Dieser Wert kann sich von der Anzahl von parallelen Prozessen unterscheiden, die angefordert wurden.|  
|external_user_name|**nvarchar**|Das Windows-Workerkonto, unter dem das Skript ausgeführt wurde.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
> [!NOTE]
>   
>  Benutzer, die externe Skripts ausführen, müssen die zusätzliche Berechtigung EXECUTE ANY EXTERNAL SCRIPT haben, aber diese dynamische Verwaltungssicht kann von Administratoren ohne diese Berechtigung verwendet werden. 
  
## <a name="remarks"></a>Hinweise  

Diese Sicht kann über die Skriptsprachen-ID gefiltert werden.

Die Sicht gibt auch das Workerkonto zurück, unter dem das Skript ausgeführt wird. Informationen zu Workerkonten, die von R-Skripts verwendet werden, finden Sie unter [Ändern des Benutzerkontenpools für SQL Server R-Dienste](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).

Die GUID, die im **external_script_request_id** -Feld zurückgegeben wird, entspricht auch dem Dateinamen des geschützten Verzeichnisses, in dem temporäre Dateien gespeichert werden. Jedes Workerkonto, z. B. MSSQLSERVER01, entspricht einer einzelnen SQL-Anmeldung oder einem einzelnen Windows-Benutzer und kann dazu verwendet werden, mehrere Skriptanforderungen auszuführen. Standardmäßig werden diese temporären Dateien nach Abschluss des angeforderten Skripts gelöscht. Wenn Sie diese Dateien für einen bestimmten Zeitraum zu Debugzwecken beibehalten müssen, können Sie das Cleanup-Flag so ändern, wie dies in diesem Thema beschrieben ist: [Konfigurieren und Verwalten von Advanced Analytics-Erweiterungen](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
 
Diese dynamische Verwaltungssicht überwacht nur die aktiven Prozesse und kann nichts zu Skripts berichten, die bereits abgeschlossen wurden. Wenn Sie die Dauer von Skripts nachverfolgen müssen, empfiehlt es sich, Informationen zur zeitlichen Steuerung in Ihrem Skript hinzuzufügen und diese Informationen als Teil der Skriptausführung zu erfassen.


## <a name="examples"></a>Beispiele  
  
### <a name="viewing-the-currently-active-r-scripts-for-a-particular-process"></a>Anzeigen der derzeit aktiven R-Skripts für einen bestimmten Prozess 
 Im folgenden Beispiel wird die Anzahl von externen Skriptausführungen angezeigt, die für die aktuelle Instanz ausgeführt werden.  
  
```  
SELECT external_script_request_id 
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests; 
```  

Ergebnisse  


external_script_request_id  |Sprache  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

