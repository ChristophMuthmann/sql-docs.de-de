---
title: Sys. remote_logins (Transact-SQL) | Microsoft Docs
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
- sys.remote_logins_TSQL
- remote_logins
- remote_logins_TSQL
- sys.remote_logins
dev_langs: TSQL
helpviewer_keywords: sys.remote_logins catalog view
ms.assetid: 38477e91-d084-4df7-b1de-b930c5580189
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0daa6c758dd1656bf3731199bd2f5b50bf90d48c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysremotelogins-transact-sql"></a>sys.remote_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro Zuordnung von Remoteanmeldenamen zurück. Diese Katalogsicht wird zum Zuordnen von eingehenden lokalen Anmeldenamen verwendet, die vorgeben, von einem entsprechenden Server zu stammen und an einen tatsächlichen lokalen Anmeldenamen gerichtet zu sein.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID des Servers in **sys.servers**. Dieser Name wird von der Verbindung des so genannten Remoteservers bereitgestellt.|  
|**NULL**|**sysname**|Der zuzuordnende Anmeldename, der von der Verbindung geliefert wird. Bei einem Wert von NULL der Anmeldename, der in der verwendeten Verbindung angegeben ist.|  
|**local_principal_id**|**int**|ID des Serverprinzipals, dem der Anmeldename zugeordnet wird. Bei einem Wert von 0 wird der Remoteanmeldename der Anmeldung mit demselben Namen zugeordnet.|  
|**modify_date**|**datetime**|Datum, an dem die verknüpfte Anmeldung zuletzt geändert wurde.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungsserver-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
