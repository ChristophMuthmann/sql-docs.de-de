---
title: Sys. dm_exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_connections_TSQL
- sys.dm_exec_connections_TSQL
- sys.dm_exec_connections
- dm_exec_connections
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_connections dynamic management view
ms.assetid: 6bd46fe1-417d-452d-a9e6-5375ee8690d8
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7c8bee848550fb2120fd02c31b505fc0b8da90b5
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmexecconnections-transact-sql"></a>sys.dm_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen über die zu dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellten Verbindungen zurück, sowie Details zu jeder der Verbindungen. Gibt die Breite Serververbindungsinformationen für SQL Server zurück. Gibt die aktuelle Datenbank-Verbindungsinformationen für SQL-Datenbank zurück.  
  
> [!NOTE]
> Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie [sys.dm_pdw_exec_connections &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|Identifiziert die Sitzung, die dieser Verbindung zugeordnet ist. Lässt NULL-Werte zu.|  
|most_recent_session_id|**int**|Stellt die Sitzungs-ID für die letzte Anforderung dar, die dieser Verbindung zugeordnet ist. (SOAP-Verbindungen können von einer anderen Sitzung erneut verwendet werden.) Lässt NULL-Werte zu.|  
|connect_time|**datetime**|Zeitstempel, der angibt, wann die Verbindung eingerichtet wurde. Lässt keine NULL-Werte zu.|  
|net_transport|**nvarchar(40)**|Gibt immer **Sitzung** Wenn eine Verbindung mehrere aktive Resultsets (MARS) aktiviert ist.<br /><br /> **Hinweis:** beschreibt das physische Transportprotokoll, das von dieser Verbindung verwendet wird. Lässt keine NULL-Werte zu.|  
|protocol_type|**nvarchar(40)**|Gibt den Protokolltyp der Nutzlast an. Zurzeit wird zwischen TDS (TSQL) und SOAP unterschieden. Lässt NULL-Werte zu.|  
|protocol_version|**int**|Die Version des Datenzugriffsprotokolls, das dieser Verbindung zugeordnet ist. Lässt NULL-Werte zu.|  
|endpoint_id|**int**|Ein Bezeichner, der beschreibt, um welchen Verbindungstyp es sich handelt. Dieser endpoint_id-Wert kann zum Abfragen der sys.endpoint-Sicht verwendet werden. Lässt NULL-Werte zu.|  
|encrypt_option|**nvarchar(40)**|Boolescher Wert, der angibt, ob die Verschlüsselung für diese Verbindung aktiviert ist. Lässt keine NULL-Werte zu.|  
|auth_scheme|**nvarchar(40)**|Gibt das mit dieser Verbindung verwendete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-/Windows-Authentifizierungsschema an. Lässt keine NULL-Werte zu.|  
|node_afinity|**smallint**|Identifiziert den Speicherknoten, zu dem diese Verbindung eine Affinität besitzt. Lässt keine NULL-Werte zu.|  
|num_reads|**int**|Anzahl der Byte-Lesevorgänge, die über diese Verbindung erfolgt sind. Lässt NULL-Werte zu.|  
|num_writes|**int**|Anzahl der Byte-Schreibvorgänge, die über diese Verbindung erfolgt sind. Lässt NULL-Werte zu.|  
|last_read|**datetime**|Zeitstempel für den letzten Lesevorgang, der über diese Verbindung erfolgt ist. Lässt NULL-Werte zu.|  
|last_write|**datetime**|Zeitstempel für den letzten Schreibvorgang, der über diese Verbindung erfolgt ist. Lässt keine NULL-Werte zu.|  
|net_packet_size|**int**|Netzwerkpaketgröße, die für die Informations- und Datenübertragung verwendet wird. Lässt NULL-Werte zu.|  
|client_net_address|**varchar(48)**|Hostadresse des Clients, der die Verbindung mit diesem Server herstellt. Lässt NULL-Werte zu.<br /><br /> Vorgängerversionen von V12 in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], diese Spalte gibt immer NULL zurück.|  
|client_tcp_port|**int**|Portnummer auf dem Clientcomputer, die dieser Verbindung zugeordnet ist. Lässt NULL-Werte zu.<br /><br /> In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] gibt diese Spalte immer NULL zurück.|  
|local_net_address|**varchar(48)**|Stellt die IP-Adresse auf dem Server dar, die die Zieladresse dieser Verbindung ist. Ist nur für Verbindungen verfügbar, die den TCP-Transportanbieter verwenden. Lässt NULL-Werte zu.<br /><br /> In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] gibt diese Spalte immer NULL zurück.|  
|local_tcp_port|**int**|Stellt den Server-TCP-Port dar, der der Zielport dieser Verbindung ist, falls die Verbindung den TCP-Transport verwendet. Lässt NULL-Werte zu.<br /><br /> In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] gibt diese Spalte immer NULL zurück.|  
|connection_id|**uniqueidentifier**|Dient zur eindeutigen Identifizierung jeder Verbindung. Lässt keine NULL-Werte zu.|  
|parent_connection_id|**uniqueidentifier**|Identifiziert die primäre Verbindung, die von der MARS-Sitzung verwendet wird. Lässt NULL-Werte zu.|  
|most_recent_sql_handle|**varbinary(64)**|Das SQL-Handle der letzten Anforderung, die über diese Verbindung ausgeführt wurde. Die most_recent_sql_handle-Spalte ist immer mit der most_recent_session_id-Spalte synchronisiert. Lässt NULL-Werte zu.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.
  
## <a name="physical-joins"></a>Physische Joins  
 ![Joins für Sys. dm_exec_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-exec-connections-1.gif "Joins für Sys. dm_exec_connections")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
||||  
|-|-|-|  
|dm_exec_sessions.session_id|dm_exec_connections.session_id|1:1|  
|dm_exec_requests.connection_id|dm_exec_connections.connection_id|n:1|  
|dm_broker_connections.connection_id|dm_exec_connections.connection_id|1:1|  
  
## <a name="examples"></a>Beispiele  
 Typische Abfrage zum Sammeln von Informationen über die eigene Verbindung einer Abfrage.  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>Siehe auch  

 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


