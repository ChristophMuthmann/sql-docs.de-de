---
title: dbo.slo_service_objectives (Azure SQL-Datenbank) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5330bc8977c0e043f27cb5f035510c5da007e0c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

    
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
|Beschreibung|**nvarchar**|Die Beschreibung des Servicelevelziels.|  
|create_date|**DateTimeOffset(7)**|Das Erstellungsdatum des Servicelevelobjekts auf dem Server.|  
|is_system|**bit**|1 = Servicelevelziel des Systems|  
|is_default|**bit**|1 = Das Servicelevelziel entspricht dem Standard-SLO.|  
|state|**tinyint**|1 = Das Servicelevelziel ist aktiviert.<br /><br /> 2 = Das Servicelevelziel ist deaktiviert.|  
|state_desc|**nvarchar**|Die Beschreibung des Servicelevelziels.|  
|metadata_version|**decimal**|Die Version des Servicelevelziels.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Premiumdatenbanken](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
