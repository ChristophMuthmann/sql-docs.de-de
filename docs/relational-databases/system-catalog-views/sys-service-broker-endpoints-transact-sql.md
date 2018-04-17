---
title: Sys. service_broker_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9bfbe05a6cef26dc891c0b2b8069c26ec4a55e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Katalogsicht enthält eine Zeile für den Service Broker-Endpunkt. Für jede Zeile in dieser Ansicht sind, besteht eine entsprechende Zeile mit dem gleichen **Endpoint_id** in der **Sys. tcp_endpoints** an, die die TCP-Konfigurationsmetadaten enthält. TCP ist das einzige für Service Broker zulässige Protokoll.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**|**--**|Erbt Spalten von [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_message_forwarding_enabled**|**bit**|Gibt an, ob die Nachrichtenweiterleitung vom Endpunkt unterstützt wird. Dies ist anfänglich auf festgelegt **0** (deaktiviert). Lässt keine NULL-Werte zu.|  
|**message_forwarding_size**|**int**|Die maximale Anzahl von Megabytes **Tempdb** Speicherplatz darf für weitergeleitete Meldungen verwendet werden. Dies ist anfänglich auf festgelegt **10**. Lässt keine NULL-Werte zu.|  
|**connection_auth**|**tinyint**|Der Typ von Verbindungsauthentifizierung, der für Verbindungen mit diesem Endpunkt erforderlich ist. Folgende Werte sind möglich:<br /><br /> **1** -NTLM<br /><br /> **2** – KERBEROS<br /><br /> **3** -AUSHANDELN<br /><br /> **4** -ZERTIFIKAT<br /><br /> **5** -NTLM, ZERTIFIKAT<br /><br /> **6** -KERBEROS, ZERTIFIKAT<br /><br /> **7** -AUSHANDELN, ZERTIFIKAT<br /><br /> **8** -ZERTIFIKAT, NTLM<br /><br /> **9** -ZERTIFIKAT, KERBEROS<br /><br /> **10** -ZERTIFIKAT, AUSHANDELN<br /><br /> Lässt keine NULL-Werte zu.|  
|**connection_auth_desc**|**nvarchar(60)**|Die Beschreibung des Types von Verbindungsauthentifizierung, der für Verbindungen mit diesem Endpunkt erforderlich ist. Folgende Werte sind möglich:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> Lässt NULL-Werte zu.|  
|**certificate_id**|**int**|Gegebenenfalls ID des für die Authentifizierung verwendeten Zertifikats.<br /><br /> 0 = Windows-Authentifizierung wird verwendet.|  
|**encryption_algorithm**|**tinyint**|Der Verschlüsselungsalgorithmus. Im folgenden sind die möglichen Werte mit ihren Beschreibungen und entsprechende DDL-Optionen.<br /><br /> **0** : NONE. Entsprechende DDL-Option: deaktiviert.<br /><br /> **1** :  RC4. Entsprechende DDL-Option: {erforderlich &#124; Required Algorithm RC4}.<br /><br /> **2** : AES. Entsprechende DDL-Option: AES-Algorithmus erforderlich.<br /><br /> **3** : NONE, RC4. Entsprechende DDL-Option: {unterstützte &#124; unterstützten Algorithmus RC4}.<br /><br /> **4** : KEINER, AES. Entsprechende DDL-Option: AES-Algorithmus unterstützt.<br /><br /> **5** : RC4, AES. Entsprechende DDL-Option: Algorithmus RC4 AES erforderlich.<br /><br /> **6** : AES, RC4. Entsprechende DDL-Option: Algorithmus AES RC4 erforderlich.<br /><br /> **7** : NONE, RC4, AES. Entsprechende DDL-Option: die RC4 AES-Algorithmus unterstützt.<br /><br /> **8** : KEINER, AES, RC4. Entsprechende DDL-Option: die AES RC4-Algorithmus unterstützt.<br /><br /> Lässt keine NULL-Werte zu.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Beschreibung der Verschlüsselung-Algorithmus. Die möglichen Werte sowie die zugehörigen DDL-Optionen sind im folgenden aufgeführt:<br /><br /> NONE: deaktiviert<br /><br /> RC4: {erforderlich &#124; Algorithmus RC4 erforderlich}<br /><br /> AES: Required Algorithm AES<br /><br /> KEINER, RC4: {unterstützt &#124; Algorithmus RC4 unterstützt}<br /><br /> KEINER, AES: Unterstützte AES-Algorithmus<br /><br /> RC4, AES: Erforderlichen Algorithmus RC4 AES<br /><br /> AES, RC4: Required Algorithm AES RC4<br /><br /> KEINER, RC4, AES: Unterstützten Algorithmus RC4 AES<br /><br /> KEINER, AES, RC4: Unterstützten Algorithmus AES RC4<br /><br /> Lässt NULL-Werte zu.|  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höheren Versionen kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
