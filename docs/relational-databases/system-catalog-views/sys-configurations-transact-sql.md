---
title: Sys.Configurations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38f44fb8d174d3fa32bea9d97e079fce0c3d1afc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede für den serverweiten Wert der Konfigurationsoption im System an.  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Eindeutige ID des Konfigurationswerts.|  
|**name**|**nvarchar(35)**|Der Name der Konfigurationsoption.|  
|**Wert**|**sql_variant**|Der für diese Option konfigurierte Wert.|  
|**minimum**|**sql_variant**|Der Mindestwert für die Konfigurationsoption.|  
|**maximum**|**sql_variant**|Der Höchstwert für die Konfigurationsoption.|  
|**value_in_use**|**sql_variant**|Ausgeführter Wert, der derzeit für diese Option wirksam ist.|  
|**Beschreibung**|**nvarchar(255)**|Beschreibung der Konfigurationsoption.|  
|**is_dynamic**|**bit**|1 = Variable, die bei Ausführung der RECONFIGURE-Anweisung wirksam wird.|  
|**is_advanced**|**bit**|1 = die Variable wird angezeigt. nur, wenn die **anzeigen Advancedoption** festgelegt ist.|  
  
 Eine Liste aller Serverkonfigurationsoptionen finden Sie [Serverkonfigurationsoptionen &#40; SQLServer &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Auf Datenbankebene-Konfigurationsoptionen finden Sie unter [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Zum Konfigurieren von Soft-NUMA finden Sie unter [Soft-NUMA &#40; SQLServer &#41; ](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Serverweite Konfiguration-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
