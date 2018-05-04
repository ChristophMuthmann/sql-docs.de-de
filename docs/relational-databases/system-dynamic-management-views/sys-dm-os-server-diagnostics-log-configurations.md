---
title: sys.dm_os_server_diagnostics_log_configurations | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations_TSQL
- dm_os_server_diagnostics_log_configurations
- dm_os_server_diagnostics_log_configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations
ms.assetid: c09ea433-d283-4f83-af69-d458aad59217
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c895d4ab88f54620f2305783d8d2e1a3699e1b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosserverdiagnosticslogconfigurations"></a>sys.dm_os_server_diagnostics_log_configurations
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt eine Zeile mit der aktuellen Konfiguration für das Diagnoseprotokoll des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusters zurück. Diese Eigenschafteneinstellungen bestimmen, ob die Diagnoseprotokollierung aktiviert oder deaktiviert ist, sowie den Speicherort, die Anzahl und die Größe der Protokolldateien.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|is_enabled|**bit**|Gibt an, ob die Protokollierung aktiviert oder deaktiviert ist.<br /><br /> 1 = Die Diagnoseprotokollierung ist aktiviert.<br /><br /> 0 = Die Diagnoseprotokollierung ist deaktiviert.|  
|max_size|**int**|Maximale Größe in Megabyte für jedes Diagnoseprotokoll. Die Standardeinstellung ist 100 MB.|  
|max_files|**int**|Maximale Anzahl von Diagnoseprotokolldateien, die auf dem Computer gespeichert werden können, bevor sie für neue Diagnoseprotokolle wiederverwendet werden.|  
|path|**nvarchar(260)**|Pfad, der den Speicherort für die Diagnoseprotokolle angibt. Der Standardspeicherort ist \<\MSSQL\Log> im Installationsordner der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert VIEW SERVER STATE-Berechtigungen für die SQL Server-Failoverclusterinstanz.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Eigenschafteneinstellungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failover-Diagnoseprotokolle mithilfe von "sys.dm_os_server_diagnostics_log_configurations" zurückgegeben.  
  
```  
SELECT <list of columns>  
FROM sys.dm_os_server_diagnostics_log_configurations;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|IS_ENABLED|PATH|MAX_SIZE|MAX_FILES|  
|-----------------|----------|---------------|----------------|  
|1|\<C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\Log >|10|10|  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Lesen des Failoverclusterinstanz-Diagnoseprotokolls](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
