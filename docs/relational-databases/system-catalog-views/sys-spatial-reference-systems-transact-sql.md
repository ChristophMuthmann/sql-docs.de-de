---
title: spatial_reference_systems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 46721d1a238c10d28c45e090ea3368775510e142
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysspatialreferencesystems-transact-sql"></a>sys.spatial_reference_systems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Listet die räumlichen Referenzsysteme (SRIDs) auf, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt werden.  

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|Das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützte SRID.|  
|authority_name|**nvarchar(128)**|Die Autorität des SRID.|  
|authorized_spatial_reference_id|**int**|Das SRID von der Stelle mit dem Namen im **Authority_name**.|  
|well_known_text|**nvarchar(4000)**|Die WKT-Darstellung des SRID.|  
|unit_of_measure|**nvarchar(128)**|Der Name der Maßeinheit.|  
|unit_conversion_factor|**float**|Die Länge der Maßeinheit in Metern.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
