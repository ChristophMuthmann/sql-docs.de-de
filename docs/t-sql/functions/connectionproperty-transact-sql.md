---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a5b023530bce0269af96918b0d578c6ca54293d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt Informationen über die Verbindungseigenschaften für die eindeutige Verbindung zurück, über die eine Anforderung eingegangen ist.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>Argumente  
*Eigenschaft*  
Die Eigenschaft der Verbindung. Für*property* sind die folgenden Werte möglich.
  
|Wert|Datentyp|Description|  
|---|---|---|
|net_transport|**nvarchar(40)**|Gibt das physische Transportprotokoll zurück, das von dieser Verbindung verwendet wird. Lässt keine NULL-Werte zu.<br /><br /> Rückgabewerte sind: **HTTP**, **Named pipe**, **Session**, **Shared memory**, **SSL**, **TCP**und **VIA**.<br /><br /> Hinweis: Gibt immer **Sitzung** Wenn eine Verbindung besteht, mehrere aktive Resultsets (MARS) aktiviert und Verbindungspooling aktiviert ist.|  
|protocol_type|**nvarchar(40)**|Gibt den Protokolltyp der Nutzlast zurück. Zurzeit wird zwischen TDS (TSQL) und SOAP unterschieden. Lässt NULL-Werte zu.|  
|auth_scheme|**nvarchar(40)**|Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierungsschema für eine Verbindung. Das Authentifizierungsschema ist entweder Windows-Authentifizierung (NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. Lässt keine NULL-Werte zu.|  
|local_net_address|**varchar(48)**|Gibt die IP-Adresse auf dem Server zurück, die die Zieladresse dieser Verbindung ist. Ist nur für Verbindungen verfügbar, die den TCP-Transportanbieter verwenden. Lässt NULL-Werte zu.|  
|local_tcp_port|**int**|Gibt den Server-TCP-Port zurück, der der Zielport dieser Verbindung ist, falls die Verbindung den TCP-Transport verwendet. Lässt NULL-Werte zu.|  
|client_net_address|**varchar(48)**|Fragt nach der Adresse des Clients, der die Verbindung mit diesem Server herstellt. Lässt NULL-Werte zu.|  
|physical_net_transport|**nvarchar(40)**|Gibt das physische Transportprotokoll zurück, das von dieser Verbindung verwendet wird. Genau, wenn für eine Verbindung Multiple Active Result Sets (MARS) aktiviert sind.|  
|\<Eine beliebige andere Zeichenfolge >||Gibt NULL zurück, wenn die Eingabe nicht gültig ist.|  
  
## <a name="remarks"></a>Hinweise  
**Local_net_address** und **Local_tcp_port** NULL in zurückgeben [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
Die zurückgegebenen Werte sind identisch mit den Optionen für die entsprechenden Spalten in der [Sys. dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md) -verwaltungssicht. Beispiel:
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>Siehe auch
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[Sys. dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  

