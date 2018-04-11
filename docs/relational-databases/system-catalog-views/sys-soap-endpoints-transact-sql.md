---
title: Sys. soap_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql-non-specified
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
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38bc05ab3d49716f2c4fc484098c4ff838bc634e
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Enthält eine Zeile für jeden Endpunkt auf dem Server, der eine Nutzlast vom Typ SOAP trägt. Für jede Zeile in dieser Sicht gibt es in der **sys.http_endpoints** -Katalogsicht eine entsprechende Zeile mit demselben **endpoint_id** -Wert, die die HTTP-Konfigurationsmetadaten enthält.  
  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**< geerbte Spalten >**||Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = Die Option BATCHES = ENABLED wurde angegeben, d. h., Ad-hoc-SQL-Batches sind auf dem Endpunkt zulässig.|  
|**wsdl_generator_procedure**|**nvarchar(776)**|Der dreiteilige Name der gespeicherten Prozedur, durch die diese Methode implementiert ist.<br /><br /> Namen von Methoden müssen der dreiteiligen Syntax entsprechen. Ein-, zwei- oder vierteilige Namen sind nicht zulässig.|  
|**default_database**|**sysname**|Der Name der Standarddatenbank, der in der Option DATABASE = angegeben ist.<br /><br /> NULL = DEFAULT wurde angegeben.|  
|**default_namespace**|**nvarchar(384)**|Der Standardnamespace im NAMESPACE angegeben = Option, oder "http://tempuri.org", wenn stattdessen DEFAULT angegeben wurde.|  
|**default_result_schema**|**tinyint**|Der Standardwert der Option SCHEMA = .<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar(60)**|Die Beschreibung des Standardwerts der Option SCHEMA = .<br /><br /> Keine<br /><br /> Standardwert|  
|**is_xml_charset_enforced**|**bit**|0 = Die Option CHARACTER_SET = SQL wurde angegeben.<br /><br /> 1 = Die Option CHARACTER_SET = XML wurde angegeben.|  
|**is_session_enabled**|**bit**|0 = Die Option SESSION = DISABLE wurde angegeben.<br /><br /> 1 = Die Option SESSION = ENABLED wurde angegeben.|  
|**session_timeout**|**int**|Der in der Option SESSION_TIMEOUT = angegebene Wert.|  
|**login_type**|**nvarchar(60)**|Die an diesem Endpunkt zulässige Art der Authentifizierung.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|Die maximal zulässige Größe des SOAP-Headers.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Endpoints Catalog Views &#40;Transact-SQL&#41; (Katalogsichten für Endpunkte &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
