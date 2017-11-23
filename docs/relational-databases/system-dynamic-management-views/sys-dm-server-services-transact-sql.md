---
title: dm_server_services (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8642cd9036fcaf7835c6dffc01f60817bdaa82bb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über die SQL-Server, Volltext- und SQL Server-Agent-Dienste in der aktuellen Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie diese dynamische Verwaltungssicht, um Statusinformationen zu diesen Diensten zu melden.  
  
 
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Name des SQL Server-, Volltext- oder SQL Server-Agent-Dienstes. Darf nicht NULL sein.|  
|startup_type|**int**|Gibt den Startmodus des Dienstes an. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> 0: andere<br />1: andere<br />2: automatische<br />3: Manual<br />4: deaktiviert<br /><br /> Lässt NULL-Werte zu.|  
|startup_desc|**nvarchar(256)**|Beschreibt den Startmodus des Diensts. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> Andere: Sonstige (Bootstart)<br />Andere: Sonstige (Systemstart)<br />Automatisch: Autostart<br />Manual: Bei Bedarf starten<br />Deaktiviert: deaktiviert<br /><br /> Lässt keine NULL-Werte zu.|  
|status|**int**|Zeigt den aktuellen Status des Diensts an. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> 1: beendet<br />2: andere (Start steht aus)<br />3: andere (Beenden steht aus)<br />4: Ausführen<br />5: andere (Fortsetzung steht aus)<br />6: andere (Anhalten steht aus)<br />7: angehalten<br /><br /> Lässt NULL-Werte zu.|  
|status_desc|**nvarchar(256)**|Beschreibt den aktuellen Status des Diensts. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> Beendet: Der Dienst wurde beendet.<br />Andere (Startvorgang steht aus): der Dienst wird gerade gestartet.<br />Andere (Beendigungsvorgang steht aus): der Dienst wird gerade beendet.<br />Wird ausgeführt: Der Dienst ausgeführt wird.<br />Andere (Fortsetzungsvorgang steht aus): der Dienst befindet sich im Status "Ausstehend".<br />Andere (Anhalten steht aus): der Dienst wird gerade angehalten.<br />Angehalten: Der Dienst ist angehalten.<br /><br /> Lässt keine NULL-Werte zu.|  
|process_id|**int**|Die Prozess-ID des Diensts. Darf nicht NULL sein.|  
|last_startup_time|**DateTimeOffset(7)**|Das Datum und die Uhrzeit, zu der der Dienst zuletzt gestartet wurde. Lässt NULL-Werte zu.|  
|service_account|**nvarchar(256)**|Das Dienstkonto, das zum Steuern des Diensts autorisiert ist. Dieses Konto kann den Dienst starten oder beenden und die Diensteigenschaften bearbeiten. Darf nicht NULL sein.|  
|filename|**nvarchar(256)**|Der Pfad und Dateiname der ausführbaren Dienstdatei. Darf nicht NULL sein.|  
|is_clustered|**nvarchar(1)**|Gibt an, ob der Dienst als Ressource eines gruppierten Servers installiert ist. Darf nicht NULL sein.|  
|cluster_nodename|**nvarchar(256)**|Der Name des Clusterknotens, auf dem der Dienst installiert ist. Lässt NULL-Werte zu.|
|instant_file_initialization_enabled|**nvarchar(1)**|**Gilt für: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 und ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Gibt an, ob die sofortige dateiinitialisierung für SQL Server-Datenbankmodul-Dienst aktiviert ist. Diese Eigenschaft gilt nicht für Dienste (Beispiel: SQL Server-Agent) als SQL Server Database Engine Services. NULL-Werte zulässt.<br /><br />Y = sofortige dateiinitialisierung für den Dienst aktiviert ist.<br /><br />N = sofortige dateiinitialisierung für den Dienst deaktiviert ist.|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW SERVER STATE`-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [dm_server_registry &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
  
