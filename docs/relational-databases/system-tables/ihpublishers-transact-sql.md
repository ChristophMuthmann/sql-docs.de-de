---
title: IHpublishers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHpublishers
- IHpublishers_TSQL
dev_langs: TSQL
helpviewer_keywords: IHpublishers system table
ms.assetid: 77007246-f10b-4b87-8edf-7afc3c2096af
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a53ef3960364ea40ccd1911f26a31270ffd9b09b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="ihpublishers-transact-sql"></a>IHpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHpublishers** -Systemtabelle enthält eine Zeile für jedes nicht - SQL Server-Verleger mithilfe des aktuellen Verteilers. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Identifiziert einen nicht - SQL Server-Verleger.|  
|**Hersteller**|**sysname**|Der Name des Herstellers für die SQL Server - Datenbank.|  
|**publisher_guid**|**uniqueidentifier**|Ein GUID, der einen Nicht-SQL Server-Verleger identifiziert.|  
|**flush_request_time**|**datetime**|Gibt das Datum und die Uhrzeit der letzten Änderung an Artikelmetadaten an, für die der Protokolllese-Agent den Metadatencache aktualisieren musste.|  
|**version**|**sysname**|Eine Textzeichenfolge, die die Version von nicht - SQL Server-Verlegers kennzeichnet.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [Sp_helpdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)  
  
  
