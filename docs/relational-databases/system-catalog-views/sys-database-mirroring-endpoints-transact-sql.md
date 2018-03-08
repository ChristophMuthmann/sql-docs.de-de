---
title: sys.database_mirroring_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b9bc0c2229fe72265957d39991f2b67a1b395f0b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für den Datenbankspiegelungs-Endpunkt einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Der datenbankspiegelungs-Endpunkt unterstützt sowohl Sitzungen zwischen Datenbank-spiegelungspartnern und Zeugen als auch Sitzungen zwischen dem primären Replikat einer Always On-verfügbarkeitsgruppe und deren sekundäre Replikate.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**|—|Erbt Spalten von **sys.endpoints** (Weitere Informationen finden Sie unter [sys.endpoints &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)).|  
|**role**|**tinyint**|Spiegelungsrolle. Folgende Werte sind möglich:<br /><br /> **0** = keine<br /><br /> **1** = Partner<br /><br /> **2** = Witness<br /><br /> **3** = all<br /><br /> Hinweis: Dieser Wert ist nur für die datenbankspiegelung relevant.|  
|**role_desc**|**nvarchar(60)**|Beschreibung der Spiegelungsrolle. Folgende Werte sind möglich:<br /><br /> **NONE**<br /><br /> **PARTNER**<br /><br /> **ZEUGEN**<br /><br /> **ALL**<br /><br /> Hinweis: Dieser Wert ist nur für die datenbankspiegelung relevant.|  
|**is_encryption_enabled**|**bit**|**1** bedeutet, dass die Verschlüsselung aktiviert ist.<br /><br /> **0** bedeutet, dass die Verschlüsselung ist deaktiviert.|  
|**connection_auth**|**tinyint**|Der Typ von Verbindungsauthentifizierung, der für Verbindungen mit diesem Endpunkt erforderlich ist. Folgende Werte sind möglich:<br /><br /> **1** -NTLM<br /><br /> **2** – KERBEROS<br /><br /> **3** -AUSHANDELN<br /><br /> **4** -ZERTIFIKAT<br /><br /> **5** -NTLM, ZERTIFIKAT<br /><br /> **6** -KERBEROS, ZERTIFIKAT<br /><br /> **7** -AUSHANDELN, ZERTIFIKAT<br /><br /> **8** -ZERTIFIKAT, NTLM<br /><br /> **9** -ZERTIFIKAT, KERBEROS<br /><br /> **10** -ZERTIFIKAT, AUSHANDELN|  
|**connection_auth_desc**|**Nvarchar (60)**|Beschreibung des Authentifizierungstyps, der für Verbindungen mit diesem Endpunkt erforderlich ist. Folgende Werte sind möglich:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|Gegebenenfalls ID des für die Authentifizierung verwendeten Zertifikats.<br /><br /> 0 = Windows-Authentifizierung wird verwendet.|  
|**encryption_algorithm**|**tinyint**|Verschlüsselungsalgorithmus. Folgende Werte sind möglich:<br /><br /> **0** : NONE<br /><br /> **1** – RC4<br /><br /> **2** – AES<br /><br /> **3** – NONE, RC4<br /><br /> **4** – KEINER, AES<br /><br /> **5** – RC4, AES<br /><br /> **6** – AES, RC4<br /><br /> **7** – NONE, RC4, AES<br /><br /> **8** – KEINER, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Beschreibung des Verschlüsselungsalgorithmus. Folgende Werte sind möglich:<br /><br /> Keine<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40; SQLServer &#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [Der Datenbankspiegelungs-Endpunkt &#40; SQLServer &#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
