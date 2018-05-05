---
title: MSdatatype_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4251479ebfbd542fa2da436bc7d3d47e7971969
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdatatype_mappings** Sicht ordnet die SQL Server-Datentypen von SQL Server - Datenbank-Managementsysteme (DBMS) verwendeten Datentypen. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|Ist der Name des DBMS. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> **MSSQLSERVER**: das Ziel ist eine SQL Server-Datenbank.<br />**ORACLE**: das Ziel ist eine Oracle-Datenbank.<br />**DB2**: das Ziel ist eine IBM DB2-Datenbank.<br />**SYBASE**: das Ziel ist eine Sybase-Datenbank.|  
|**sql_type**|**nvarchar(128)**|Ist der SQL Server-Datentyp.|  
|**dest_type**|**nvarchar(128)**|Ist der Name des nicht - SQL Server-Datentyps.|  
|**dest_prec**|**bigint**|Ist die Genauigkeit des Datentyps nicht - SQL Server.|  
|**dest_create_params**|**int**|Nur interne Verwendung.|  
|**dest_nullable**|**bit**|Ist, wenn der nicht - SQL Server-Datentyp einen NULL-Wert unterstützt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Angeben von Datentypzuordnungen für einen Oracle-Verleger](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
