---
title: dm_db_mirroring_connections (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- sys.dm_db_mirroring_connections
- dm_db_mirroring_connections
- sys.dm_db_mirroring_connections_TSQL
- dm_db_mirroring_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_mirroring_connections dynamic management view
ms.assetid: e4df91b6-0240-45d0-ae22-cb2c0d52e0b3
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a89678342234f6ff88ba67687f4b81900e7cf733
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="database-mirroring---sysdmdbmirroringconnections"></a>Datenbankspiegelung - dm_db_mirroring_connections
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt für jede für die Datenbankspiegelung hergestellte Verbindung eine Zeile zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|Bezeichner der Verbindung.|  
|**transport_stream_id**|**uniqueidentifier**|Der Bezeichner der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Netzwerkschnittstelle (SNI)-Verbindung, die von dieser Verbindung für die TCP/IP-Kommunikation verwendet.|  
|**state**|**smallint**|Aktueller Verbindungsstatus. Mögliche Werte:<br /><br /> 1 = NEW<br /><br /> 2 = CONNECTING<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = GESCHLOSSEN|  
|**state_desc**|**nvarchar(60)**|Aktueller Verbindungsstatus. Mögliche Werte:<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|Datum und Uhrzeit der Verbindungseröffnung.|  
|**login_time**|**datetime**|Datum und Uhrzeit der erfolgreichen Verbindungsanmeldung.|  
|**authentication_method**|**nvarchar(128)**|Name der Windows-Authentifizierungsmethode, z. B. NTLM oder KERBEROS. Dieser Wert stammt von Windows.|  
|**principal_name**|**nvarchar(128)**|Anmeldename, der auf Verbindungsberechtigungen überprüft wurde. Bei der Windows-Authentifizierung handelt es sich bei diesem Wert um den Remotebenutzernamen. Bei der Zertifikatsauthentifizierung handelt es sich bei diesem Wert um den Besitzer des Zertifikats.|  
|**remote_user_name**|**nvarchar(128)**|Name des Peer-Benutzers aus der anderen Datenbank, die von der Windows-Authentifizierung verwendet wird.|  
|**last_activity_time**|**datetime**|Datum und Uhrzeit für die letzte Verwendung der Verbindung zum Senden oder Empfangen von Informationen.|  
|**is_accept**|**bit**|Gibt an, ob die Verbindung ursprünglich von der Remoteseite stammt.<br /><br /> 1 = Die Verbindung ist eine Anforderung, die von der Remoteinstanz angenommen wurde.<br /><br /> 0 = Die Verbindung wurde von der lokalen Instanz gestartet.|  
|**login_state**|**smallint**|Status des Anmeldeprozesses für diese Verbindung. Mögliche Werte:<br /><br /> 0 = INITIAL<br /><br /> 1 = WAIT LOGIN NEGOTIATE<br /><br /> 2 = ONE ISC<br /><br /> 3 = ONE ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = TWO ASC<br /><br /> 6 = WAIT ISC Confirm<br /><br /> 7 = WAIT ASC Confirm<br /><br /> 8 = WAIT REJECT<br /><br /> 9 = WAIT PRE-MASTER SECRET<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = WAIT ARBITRATION<br /><br /> 12 = ONLINE<br /><br /> 13 = ERROR|  
|**login_state_desc**|**nvarchar(60)**|Aktueller Anmeldestatus des Remotecomputers. Mögliche Werte:<br /><br /> Verbindungshandshake wird initialisiert.<br /><br /> Verbindungshandshake wartet auf Anmeldungsaushandlungs-Meldung.<br /><br /> Verbindungshandshake hat Sicherheitskontext zur Authentifizierung initialisiert und gesendet.<br /><br /> Verbindungshandshake hat Sicherheitskontext zur Authentifizierung empfangen und akzeptiert.<br /><br /> Verbindungshandshake hat Sicherheitskontext zur Authentifizierung initialisiert und gesendet. Ein optionaler Mechanismus ist für das Authentifizieren der Peers verfügbar.<br /><br /> Verbindungshandshake hat Sicherheitskontext zur Authentifizierung empfangen und gesendet. Ein optionaler Mechanismus ist für das Authentifizieren der Peers verfügbar.<br /><br /> Verbindungshandshake wartet auf Meldung zur Bestätigung der Sicherheitskontextinitialisierung.<br /><br /> Verbindungshandshake wartet auf Meldung zur Bestätigung der Sicherheitskontextannahme.<br /><br /> Verbindungshandshake wartet auf SSPI-Ablehnungsmeldung zur fehlgeschlagenen Authentifizierung.<br /><br /> Verbindungshandshake wartet auf Meldung für Vorstufe des geheimen Hauptschlüssels.<br /><br /> Verbindungshandshake wartet auf Überprüfungsmeldung.<br /><br /> Verbindungshandshake wartet auf Vermittlungsmeldung.<br /><br /> Verbindungshandshake wurde abgeschlossen und ist online (bereit) für Nachrichtenaustausch.<br /><br /> Verbindungsfehler.|  
|**peer_certificate_id**|**int**|Das lokale Objekt-ID des von der Remoteinstanz zur Authentifizierung verwendete Zertifikats. Der Besitzer dieses Zertifikats muss über CONNECT-Berechtigungen für den Endpunkt der Datenbankspiegelung verfügen.|  
|**encryption_algorithm**|**smallint**|Der für diese Verbindung verwendete Verschlüsselungsalgorithmus. Lässt NULL-Werte zu. Mögliche Werte:<br /><br /> **Wert:** 0<br /><br /> **Beschreibung:** None<br /><br /> **DDL-Option:** deaktiviert<br /><br /> **Wert:** 1<br /><br /> **Beschreibung:** RC4<br /><br /> **DDL-Option:** {erforderlich &#124; Required Algorithm RC4}<br /><br /> **Wert:** 2<br /><br /> **Beschreibung:** AES<br /><br /> **DDL-Option:** Required Algorithm AES<br /><br /> **Wert:** 3<br /><br /> **Beschreibung:** None, RC4<br /><br /> **DDL-Option:** {unterstützte &#124; unterstützte RC4-Algorithmus}<br /><br /> **Wert:** 4<br /><br /> **Beschreibung:** keiner, AES<br /><br /> **DDL-Option:** unterstützte RC4-Algorithmus<br /><br /> **Wert:** 5<br /><br /> **Beschreibung:** RC4, AES<br /><br /> **DDL-Option:** Required Algorithm AES RC4<br /><br /> **Wert:** 6<br /><br /> **Beschreibung:** AES, RC4<br /><br /> **DDL-Option:** Algorithmus AES RC4 erforderlich<br /><br /> **Wert:** 7<br /><br /> **Beschreibung:** NONE, RC4, AES<br /><br /> **DDL-Option:** unterstützten Algorithmus RC4 AES<br /><br /> **Wert:** 8<br /><br /> **Beschreibung:** keiner, AES, RC4<br /><br /> **DDL-Option:** unterstützte AES RC4-Algorithmus<br /><br /> **Hinweis:** der RC4-Algorithmus wird nur für Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höhere Versionen mit RC4 oder RC4_128 verschlüsseltes Material kann entschlüsselt werden in jedem Kompatibilitätsgrad.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Textdarstellung des Verschlüsselungsalgorithmus. Lässt NULL-Werte zu. Mögliche Werte:<br /><br /> **Beschreibung:** None<br /><br /> **DDL-Option:** deaktiviert<br /><br /> **Beschreibung:** RC4<br /><br /> **DDL-Option:** {erforderlich &#124; Algorithmus RC4 erforderlich}<br /><br /> **Beschreibung:** AES<br /><br /> **DDL-Option:** erforderlich AES-Algorithmus<br /><br /> **Beschreibung:** NONE, RC4<br /><br /> **DDL-Option:** {unterstützt &#124; Algorithmus RC4 unterstützt}<br /><br /> **Beschreibung:** keiner, AES<br /><br /> **DDL-Option:** Algorithmus RC4 unterstützt<br /><br /> **Beschreibung:** RC4, AES<br /><br /> **DDL-Option:** erforderlich Algorithmus RC4 AES<br /><br /> **Beschreibung:** AES, RC4<br /><br /> **DDL-Option:** Algorithmus AES RC4 erforderlich<br /><br /> **Beschreibung:** NONE, RC4, AES<br /><br /> **DDL-Option:** unterstützten Algorithmus RC4 AES<br /><br /> **Beschreibung:** keiner, AES, RC4<br /><br /> **DDL-Option:** Algorithmus AES RC4 unterstützt|  
|**receives_posted**|**smallint**|Die Anzahl asynchroner Netzwerkempfangsvorgänge, die für diese Verbindung noch nicht abgeschlossen wurden.|  
|**is_receive_flow_controlled**|**bit**|Angabe, ob Netzwerkempfangsvorgänge aus Gründen der Datenflusskontrolle verschoben wurden, da das Netzwerk ausgelastet ist.<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|Die Anzahl asynchroner Netzwerksendevorgänge, die für diese Verbindung noch nicht abgeschlossen wurden.|  
|**is_send_flow_controlled**|**bit**|Angabe, ob Netzwerksendevorgänge aus Gründen der Datenflusskontrolle verschoben wurden, da das Netzwerk ausgelastet ist.<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|Die Gesamtanzahl der von dieser Verbindung gesendeten Bytes.|  
|**total_bytes_received**|**bigint**|Die Gesamtanzahl der von dieser Verbindung empfangenen Bytes.|  
|**total_fragments_sent**|**bigint**|Die Gesamtanzahl der von dieser Verbindung gesendeten Datenspiegelungs-Nachrichtenfragmente.|  
|**total_fragments_received**|**bigint**|Die Gesamtanzahl der von dieser Verbindung empfangenen Datenspiegelungs-Nachrichtenfragmente.|  
|**total_sends**|**bigint**|Gesamtanzahl der Anforderungen, die von dieser Verbindung ausgegebenen gesendet werden.|  
|**total_receives**|**bigint**|Die Gesamtanzahl der von dieser Verbindung ausgegebenen Netzwerkempfangsanforderungen.|  
|**peer_arbitration_id**|**uniqueidentifier**|Interner Bezeichner für den Endpunkt. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="physical-joins"></a>Physische Joins  
 ![Joins für Sys. join_dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-db-mirroring-connections.gif "Join für Sys. join_dm_db_mirroring_connections")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|**dm_db_mirroring_connections.connection_id**|**dm_exec_connections.connection_id**|1:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
