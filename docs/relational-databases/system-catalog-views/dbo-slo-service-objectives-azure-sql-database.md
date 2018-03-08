---
title: dbo.slo_service_objectives (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a5d3a911aa1ffa5088f2a817c2434c98eb7cbe3
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2018
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  Dieses Feature ist in einem vorschauzustand und ist veraltet [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12. Erstellen Sie keine Abhängigkeit von der spezifischen Implementierung dieser Funktion, da die Funktion in zukünftigen Versionen ggf. geändert oder entfernt werden kann.  
  
 Gibt die Servicelevelziel-Informationen (Service Level Objective, SLO) zum aktuellen Server zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11.|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|objective_id|**uniqueidentifier**|Die ID des Servicelevelziels.|  
|name|**sysname**|Der Name des Servicelevelziels.|  
|description|**nvarchar**|Die Beschreibung des Servicelevelziels.|  
|create_date|**datetimeoffset(7)**|Das Erstellungsdatum des Servicelevelobjekts auf dem Server.|  
|is_system|**bit**|1 = Servicelevelziel des Systems|  
|is_default|**bit**|1 = Das Servicelevelziel entspricht dem Standard-SLO.|  
|state|**tinyint**|1 = Das Servicelevelziel ist aktiviert.<br /><br /> 2 = Das Servicelevelziel ist deaktiviert.|  
|state_desc|**nvarchar**|Die Beschreibung des Servicelevelziels.|  
|metadata_version|**decimal**|Die Version des Servicelevelziels.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Premiumdatenbanken](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
