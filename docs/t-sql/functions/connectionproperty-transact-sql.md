---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95c95ad472c5b5d4cb5420fa3b0da8f88053c0c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt Informationen über die Verbindungseigenschaften für die eindeutige Verbindung zurück, über die eine Anforderung eingegangen ist.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>Argumente  
*property*  
Die Eigenschaft der Verbindung. Für*property* sind die folgenden Werte möglich.
  
|value|Datentyp|Description|  
|---|---|---|
|net_transport|**nvarchar(40)**|Gibt das physische Transportprotokoll zurück, das von dieser Verbindung verwendet wird. Lässt keine NULL-Werte zu.<br /><br /> Rückgabewerte sind: **HTTP**, **Named pipe**, **Session**, **Shared memory**, **SSL**, **TCP**und **VIA**.<br /><br /> Hinweis: Es wird stets **Session** zurückgegeben, wenn für eine Verbindung „mehrere aktive Resultsets“ (MARS) und Verbindungs-Pooling aktiviert ist.|  
|protocol_type|**nvarchar(40)**|Gibt den Protokolltyp der Nutzlast zurück. Zurzeit wird zwischen TDS (TSQL) und SOAP unterschieden. Lässt NULL-Werte zu.|  
|auth_scheme|**nvarchar(40)**|Gibt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierungsschema für eine Verbindung zurück. Das Authentifizierungsschema ist entweder Windows-Authentifizierung (NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. Lässt keine NULL-Werte zu.|  
|local_net_address|**varchar(48)**|Gibt die IP-Adresse auf dem Server zurück, die die Zieladresse dieser Verbindung ist. Ist nur für Verbindungen verfügbar, die den TCP-Transportanbieter verwenden. Lässt NULL-Werte zu.|  
|local_tcp_port|**int**|Gibt den Server-TCP-Port zurück, der der Zielport dieser Verbindung ist, falls die Verbindung den TCP-Transport verwendet. Lässt NULL-Werte zu.|  
|client_net_address|**varchar(48)**|Fragt nach der Adresse des Clients, der die Verbindung mit diesem Server herstellt. Lässt NULL-Werte zu.|  
|physical_net_transport|**nvarchar(40)**|Gibt das physische Transportprotokoll zurück, das von dieser Verbindung verwendet wird. Genau, wenn für eine Verbindung Multiple Active Result Sets (MARS) aktiviert sind.|  
|\<beliebige andere Zeichenfolge>||Gibt NULL zurück, wenn die Eingabe nicht gültig ist.|  
  
## <a name="remarks"></a>Remarks  
**local_net_address** und **local_tcp_port** geben in [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] NULL zurück.
  
Die zurückgegebenen Werte sind mit den Optionen identisch, die für die entsprechenden Spalten in der dynamischen Verwaltungssicht [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md) angezeigt werden. Zum Beispiel:
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>Siehe auch
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
