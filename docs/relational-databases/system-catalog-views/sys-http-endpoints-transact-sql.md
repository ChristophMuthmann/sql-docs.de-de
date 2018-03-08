---
title: Sys. http_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.http_endpoints
- http_endpoints
- sys.http_endpoints_TSQL
- http_endpoints_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.http_endpoints catalog view
ms.assetid: 16f59695-ecd9-457e-8874-055af63f8ea7
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af5140f2389501a10a9228c2e133441f072c2efc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syshttpendpoints-transact-sql"></a>sys.http_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Endpunkt auf dem Server, der das HTTP-Protokoll verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**< geerbte Spalten >**||Erbt Spalten von [sys.endpoints &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**Website**|**vom Datentyp nvarchar(128)**|Name des Hostcomputers für die Site, wie in der SITE =-Option angegeben.|  
|**url_path**|**nvarchar(4000)**|Nur den Pfad betreffender Teil der URL für diesen HTTP-Endpunkt, wie in der PATH =-Option angegeben.|  
|**is_clear_port_enabled**|**bit**|1 = CLEAR PORT ist mithilfe der PORT = CLEAR-Option aktiviert.|  
|**CLEAR_PORT**|**int**|Die in der CLEAR PORT =-Option angegebene Anschlussnummer.<br /><br /> NULL = Nicht angegeben.|  
|**is_ssl_port_enabled**|**bit**|1 = SSL PORT ist mithilfe der PORT = SSL-Option aktiviert.|  
|**SSL_PORT**|**int**|Der in der SSL PORT =-Option angegebene Wert für die Anschlussnummer.<br /><br /> NULL = Nicht angegeben.|  
|**is_anonymous_enabled**|**bit**|1 = Anonymer Zugriff ist mithilfe der AUTHENTICATION = ANONYMOUS-Option aktiviert.|  
|**is_basic_auth_enabled**|**bit**|1 = Standardauthentifizierung ist mithilfe der AUTHENTICATION = BASIC-Option aktiviert.|  
|**is_digest_auth_enabled**|**bit**|1 = Digestauthentifizierung ist mithilfe der AUTHENTICATION = DIGEST-Option aktiviert.|  
|**is_kerberos_auth_enabled**|**bit**|1 = Integrierte Authentifizierung ist mithilfe der AUTHENTICATION = KERBEROS-Option aktiviert.|  
|**is_ntlm_auth_enabled**|**bit**|1 = Integrierte Authentifizierung ist mithilfe der AUTHENTICATION = NTLM-Option aktiviert.|  
|**is_integrated_auth_enabled**|**bit**|1 = Integrierte Authentifizierung ist mithilfe der AUTHENTICATION = INTEGRATED-Option aktiviert.|  
|**authorization_realm**|**vom Datentyp nvarchar(128)**|Hinweis, der als Teil der HTTP-Digestauthentifizierungsabfrage an den Client zurückgegeben wird. Der Wert der AUTH REALM-Option.<br /><br /> Ist NULL, wenn nichts angegeben ist oder wenn die Digestauthentifizierung deaktiviert ist.|  
|**DEFAULT_LOGON_DOMAIN**|**vom Datentyp nvarchar(128)**|Standardanmeldedomäne, wenn die Standardauthentifizierung aktiviert wird. Der Wert der DEFAULT LOGON DOMAIN-Option.<br /><br /> Ist NULL, wenn nichts angegeben ist oder wenn die Standardauthentifizierung deaktiviert ist.|  
|**is_compression_enabled**|**bit**|1 = Die COMPRESSION = ENABLED-Option ist festgelegt.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Endpunkte-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
