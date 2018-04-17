---
title: Sys.Endpoints (Transact-SQL) | Microsoft Docs
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
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce88472ec2efd0d466c079c85c351e364baa3db0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile pro im System erstellten Endpunkt. Es gibt immer jeweils genau einen SYSTEM-Endpunkt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name des Endpunkts. Ist eindeutig innerhalb des Servers. Lässt keine NULL-Werte zu.|  
|**endpoint_id**|**int**|ID des Endpunkts. Ist eindeutig innerhalb des Servers. Ein Endpunkt mit einer ID kleiner 65536 ist ein Systemendpunkt. Lässt keine NULL-Werte zu.|  
|**principal_id**|**int**|ID des Serverprinzipals, der diesen Endpunkt erstellt hat und besitzt. Lässt NULL-Werte zu.|  
|**Protokoll**|**tinyint**|Endpunktprotokoll.<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = Named Pipes<br /><br /> 4 = Gemeinsam genutzter Speicherbereich<br /><br /> 5 = Virtual Interface Architecture (VIA)<br /><br /> Lässt keine NULL-Werte zu.|  
|**protocol_desc**|**nvarchar(60)**|Beschreibung des Endpunktprotokolls. Lässt NULL-Werte zu. Einer der folgenden Werte:<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **ÜBER** Hinweis: das VIA-Protokoll ist veraltet. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**type**|**tinyint**|Nutzlasttyp des Endpunkts.<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> Lässt keine NULL-Werte zu.|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Endpunkt-Nutzlasttyps. Lässt NULL-Werte zu. Einer der folgenden Werte:<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**state**|**tinyint**|Der Endpunktstatus.<br /><br /> 0 = STARTED: Anforderungen werden überwacht und verarbeitet.<br /><br /> 1 = STOPPED: Anforderungen werden überwacht, aber nicht verarbeitet.<br /><br /> 2 = DISABLED: Keine Überwachung.<br /><br /> Die Standardstatus lautet 1. Lässt NULL-Werte zu.|  
|**state_desc**|**nvarchar(60)**|Beschreibung des Endpunktstatus.<br /><br /> STARTED = Anforderungen werden überwacht und verarbeitet.<br /><br /> STOPPED = Anforderungen werden überwacht, aber nicht verarbeitet.<br /><br /> DISABLED = Keine Überwachung.<br /><br /> Der Standardstatus lautet STOPPED.<br /><br /> Lässt NULL-Werte zu.|  
|**is_admin_endpoint**|**bit**|Gibt an, ob der Endpunkt Verwaltungszwecken dient.<br /><br /> 0 = Kein Verwaltungsendpunkt.<br /><br /> 1 = Der Endpunkt ist ein Verwaltungsendpunkt.<br /><br /> Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Endpoints Catalog Views &#40;Transact-SQL&#41; (Katalogsichten für Endpunkte &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
