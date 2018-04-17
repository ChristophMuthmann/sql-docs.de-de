---
title: MSdistpublishers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc2adcd101a2f974b441cef792668dcd61c25d4c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Die **MSdistpublishers** Tabelle enthält eine Zeile für jeden vom lokalen Verteiler unterstützten Remoteverleger. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name des Verlegerverteilers.|  
|**distribution_db**|**sysname**|Der Name der Verteilungsdatenbank.|  
|**working_directory**|**nvarchar(255)**|Der Name des Arbeitsverzeichnisses zum Speichern von Daten- und Schemadateien für die Veröffentlichung verwendet werden soll.|  
|**security_mode**|**int**|Der auf dem Verteiler implementierte Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.<br /><br /> **1** = Windows-Authentifizierung.|  
|**login**|**sysname**|Die Anmelde-ID für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**password**|**nvarchar(524)**|Das (verschlüsselte) Kennwort für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.|  
|**Aktive**|**bit**|Zeigt an, ob der lokale Verteiler zurzeit vom Remoteverleger verwendet wird.|  
|**Vertrauenswürdige**|**bit**|Zeigt an, ob auf dem Remoteverleger dasselbe Kennwort wie auf dem lokalen Verteiler verwendet wird:<br /><br /> **0** = ein Kennwort ist erforderlich, auf dem Remoteverleger eine Verbindung mit dem Verteiler herstellen.<br /><br /> **1** = Nein Kennwort ist erforderlich.|  
|**Drittanbieter**|**bit**|Gibt an, ob es sich bei dem Verleger um eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation handelt:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installation. **1** = heterogene Datenquelle.|  
|**publisher_type**|**sysname**|Der Typ des Verlegers:<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.<br /><br /> **ORACLE** = standard Oracle-Verleger.<br /><br /> **ORACLE-GATEWAY** = Oracle Gateway-Verleger.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
