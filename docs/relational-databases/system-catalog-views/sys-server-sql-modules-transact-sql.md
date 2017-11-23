---
title: Sys. server_sql_modules (Transact-SQL) | Microsoft Docs
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
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs: TSQL
helpviewer_keywords: sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2056568390fc8fa7ca7e03ee7df8ace39627ca5f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysserversqlmodules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält den SQL-Modulsatz für Trigger vom Typ TR auf Serverebene. Sie können diese Beziehung mit sys.server_triggers verknüpfen. Das Tupel (object_id) ist der Schlüssel der Beziehung.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Ein FOREIGN KEY-Verweis zurück auf den Trigger auf Serverebene, wo dieses Modul definiert ist.|  
|**Definition**|**nvarchar(max)**|Der SQL-Text, der dieses Modul definiert.<br /><br /> NULL = Verschlüsselt.|  
|**uses_ansi_nulls**|**bit**|Beim Erstellen des Moduls war die Option SET ANSI NULLS auf ON festgelegt.|  
|**uses_quoted_identifier**|**bit**|Beim Erstellen des Moduls war die Option SET QUOTED IDENTIFIER auf ON festgelegt.|  
|**execute_as_principal_id**|**int**|ID des Serverprinzipals, der mit EXECUTE AS verwendet wird.<br /><br /> NULL als Standard oder bei EXECUTE AS CALLER<br /><br /> ID des angegebenen Prinzipals bei Ausführen von AS SELF EXECUTE AS-Prinzipal-2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
