---
title: Sys.sysservers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95f88c44e0501fab834bb476e0350cf48bc91757
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Server, auf den eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als OLE DB-Datenquelle zugreifen kann.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|ID (nur für lokale Verwendung) des Remoteservers.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|Name des Servers.|  
|**srvproduct**|**sysname**|Produktname für den Remoteserver.|  
|**providername**|**nvarchar(128)**|Name des OLE DB-Anbieters für den Zugriff auf diesen Server.|  
|**datasource**|**nvarchar(4000)**|OLE DB-Datenquellenwert.|  
|**location**|**nvarchar(4000)**|OLE DB-Speicherortwert.|  
|**providerstring**|**nvarchar(4000)**|Zeichenfolgenwert des OLE DB-Anbieters.|  
|**schemadate**|**datetime**|Datum, an dem diese Zeile zuletzt aktualisiert wurde.|  
|**topologyx**|**int**|Wird nicht verwendet.|  
|**topologyy**|**int**|Wird nicht verwendet.|  
|**catalog**|**sysname**|Katalog, der beim Herstellen einer Verbindung mit einem OLE DB-Anbieter verwendet wird.|  
|**srvcollation**|**sysname**|Die Sortierung des Servers.|  
|**connecttimeout**|**int**|Timeouteinstellung für die Serververbindung.|  
|**querytimeout**|**int**|Timeouteinstellung für Abfragen auf den Server.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = Server ist ein Remoteserver.<br /><br /> 0 = Server ist ein Verbindungsserver.|  
|**rpc**|**bit**|1 =  **sp_serveroption@rpc**  festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@rpc**  festgelegt **"false"** oder **deaktiviert**.|  
|**pub**|**bit**|1 =  **sp_serveroption@pub**  festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@pub**  festgelegt **"false"** oder **deaktiviert**.|  
|**sub**|**bit**|1 =  **sp_serveroption@sub**  festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@sub**  festgelegt **"false"** oder **deaktiviert**.|  
|**dist**|**bit**|1 =  **sp_serveroption@dist**  festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@dist**  festgelegt **"false"** oder **deaktiviert**.|  
|**dpub**|**bit**|1 =  **sp_serveroption@dpub**  festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@dpub**  festgelegt **"false"** oder **deaktiviert**.|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc out** festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@rpc out** festgelegt **"false"** oder **deaktiviert**.|  
|**dataaccess**|**bit**|1 =  **sp_serveroption@data Zugriff** festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@data Zugriff** festgelegt **"false"** oder **deaktiviert**.|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation kompatibel** festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@collation kompatibel** festgelegt **"false"** oder **deaktiviert**.|  
|**system**|**bit**|1 =  **sp_serveroption@system**  festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@system**  festgelegt **"false"** oder **deaktiviert**.|  
|**useremotecollation**|**bit**|1 =  **sp_serveroption@remote Sortierung** festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@remote Sortierung** festgelegt **"false"** oder **deaktiviert**.|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy schemaüberprüfung** festgelegt **"true"** oder **auf**.<br /><br /> 0 =  **sp_serveroption@lazy schemaüberprüfung** festgelegt **"false"** oder **deaktiviert**.|  
|**collation**|**sysname**|Server-Sortierung als Satz von  **sp_serveroption@collation Namen**.|  
|**nonsqlsub**|bit|0 = Server ist eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = Server ist keine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
