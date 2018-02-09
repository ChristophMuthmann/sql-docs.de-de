---
title: Sys.sysusers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 661d42fbc8b55250ac38fb84e44faa33701c20b2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jede [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzer, Windows-Gruppe [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Benutzer oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Rolle in der Datenbank.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**uid**|**smallint**|In dieser Datenbank eindeutiger Benutzername.<br /><br /> 1 = Datenbankbesitzer<br /><br /> Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl von Benutzern und Rollen 32.767 übersteigt.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|Der in dieser Datenbank eindeutige Benutzer- oder Gruppenname.|  
|**sid**|**varbinary(85)**|Sicherheitsbezeichner für diesen Eintrag.|  
|**roles**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|Datum, an dem das Konto hinzugefügt wurde.|  
|**updatedate**|**datetime**|Datum, an dem das Konto zuletzt geändert wurde.|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Führt zu einem Überlauf oder gibt NULL zurück, wenn die Anzahl von Benutzern und Rollen 32.767 übersteigt.|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**smallint**|ID der Gruppe, zu der dieser Benutzer gehört. Wenn **uid** mit **gid**identisch ist, definiert dieser Eintrag eine Gruppe. Führt zu einem Überlauf oder gibt NULL zurück, wenn die kombinierte Anzahl von Gruppen und Benutzern 32.767 übersteigt.|  
|**environ**|**varchar(255)**|Reserviert.|  
|**hasdbaccess**|**int**|1 = Konto hat Datenbankzugriff.|  
|**islogin**|**int**|1 = Konto ist ein Windows-Gruppe, die Windows-Benutzer oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Benutzer mit einem Anmeldekonto.|  
|**isntname**|**int**|1 = Konto ist eine Windows-Gruppe oder ein Windows-Benutzer.|  
|**isntgroup**|**int**|1 = Konto ist eine Windows-Gruppe.|  
|**isntuser**|**int**|1 = Konto ist ein Windows-Benutzer.|  
|**issqluser**|**int**|1 = Konto ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer.|  
|**isaliased**|**int**|1 = Konto wird als Alias für einen anderen Benutzer verwendet.|  
|**issqlrole**|**int**|1 = Konto ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rolle.|  
|**isapprole**|**int**|1 = Konto ist eine Anwendungsrolle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
