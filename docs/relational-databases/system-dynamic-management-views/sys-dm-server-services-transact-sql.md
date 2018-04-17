---
title: dm_server_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8879e4d23c4e74aaa39649b03e59d5303f42e658
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über die SQL-Server, Volltext- und SQL Server-Agent-Dienste in der aktuellen Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie diese dynamische Verwaltungssicht, um Statusinformationen zu diesen Diensten zu melden.  
  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Der Name der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Volltext- oder SQL Server-Agent-Dienst. Lässt keine NULL-Werte zu.|  
|startup_type|**int**|Gibt den Startmodus des Dienstes an. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> 0: andere<br />1: andere<br />2: automatische<br />3: Manual<br />4: deaktiviert<br /><br /> Lässt NULL-Werte zu.|  
|startup_desc|**nvarchar(256)**|Beschreibt den Startmodus des Diensts. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> Andere: Sonstige (Bootstart)<br />Andere: Sonstige (Systemstart)<br />Automatisch: Autostart<br />Manual: Bei Bedarf starten<br />Deaktiviert: deaktiviert<br /><br /> Lässt keine NULL-Werte zu.|  
|status|**int**|Zeigt den aktuellen Status des Diensts an. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> 1: beendet<br />2: andere (Start steht aus)<br />3: andere (Beenden steht aus)<br />4: Ausführen<br />5: andere (Fortsetzung steht aus)<br />6: andere (Anhalten steht aus)<br />7: angehalten<br /><br /> Lässt NULL-Werte zu.|  
|status_desc|**nvarchar(256)**|Beschreibt den aktuellen Status des Diensts. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> Beendet: Der Dienst wurde beendet.<br />Andere (Startvorgang steht aus): der Dienst wird gerade gestartet.<br />Andere (Beendigungsvorgang steht aus): der Dienst wird gerade beendet.<br />Wird ausgeführt: Der Dienst ausgeführt wird.<br />Andere (Fortsetzungsvorgang steht aus): der Dienst befindet sich im Status "Ausstehend".<br />Andere (Anhalten steht aus): der Dienst wird gerade angehalten.<br />Angehalten: Der Dienst ist angehalten.<br /><br /> Lässt keine NULL-Werte zu.|  
|process_id|**int**|Die Prozess-ID des Diensts. Lässt keine NULL-Werte zu.|  
|last_startup_time|**datetimeoffset(7)**|Das Datum und die Uhrzeit, zu der der Dienst zuletzt gestartet wurde. Lässt NULL-Werte zu.|  
|service_account|**nvarchar(256)**|Das Dienstkonto, das zum Steuern des Diensts autorisiert ist. Dieses Konto kann den Dienst starten oder beenden und die Diensteigenschaften bearbeiten. Lässt keine NULL-Werte zu.|  
|filename|**nvarchar(256)**|Der Pfad und Dateiname der ausführbaren Dienstdatei. Lässt keine NULL-Werte zu.|  
|is_clustered|**nvarchar(1)**|Gibt an, ob der Dienst als Ressource eines gruppierten Servers installiert ist. Lässt keine NULL-Werte zu.|  
|cluster_nodename|**nvarchar(256)**|Der Name des Clusterknotens, auf dem der Dienst installiert ist. Lässt NULL-Werte zu.|
|instant_file_initialization_enabled|**nvarchar(1)**|Gibt an, ob die sofortige dateiinitialisierung aktiviert ist, für die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Dienst.<br /><br />Y = sofortige dateiinitialisierung für den Dienst aktiviert ist.<br /><br />N = sofortige dateiinitialisierung für den Dienst deaktiviert ist.<br /><br /> Lässt NULL-Werte zu.<br /><br /> **Hinweis:** gilt nicht für andere Dienste wie SQL Server-Agent.<br /><br /> **Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (beginnend mit [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 über über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|  

## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW SERVER STATE`-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
