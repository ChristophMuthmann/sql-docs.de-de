---
title: MSdbms_datatype (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs: TSQL
helpviewer_keywords: MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd690436908a61b43b4e7af829e8bc3528fd5305
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdbms_datatype** Tabelle enthält die vollständige Liste der systemeigenen Datentypen in jeder unterstützten Datenbank-Managementsystem (DBMS) als Verleger oder Abonnenten in heterogenen Datenbankreplikation verwendet. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|Identifiziert jeden eindeutigen Datentyp.|  
|**dbms_id**|**int**|Identifiziert das DBMS, zu dem der Typ gehört.|  
|**Typ**|**sysname**|Der Name des Datentyps (systemeigen).|  
|**CreateParams**|**int**|Das Bitmap, das beschreibt, welche Kombination aus Länge, Genauigkeit und Dezimalstellen für jeden Datentyp gilt:<br /><br /> **0 x 1** = mit einfacher Genauigkeit.<br /><br /> **0 x 2** = Skalierung.<br /><br /> **0 x 4** = Länge.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Tabelle enthält Einträge für SQL Server-Datentypen, da eine Instanz von SQL Server in einer nicht - SQL Server-Datenbank abonnieren und auf einen nicht - SQL Server-Abonnenten veröffentlichen kann.  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Angeben von Datentypzuordnungen für einen Oracle-Verleger](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
