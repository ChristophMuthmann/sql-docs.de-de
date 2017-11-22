---
title: Sp_pdw_database_encryption_regenerate_system_keys (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 94f45c520397c608845e9bd07ec4aed173d1fd91
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sppdwdatabaseencryptionregeneratesystemkeys-sql-data-warehouse"></a>Sp_pdw_database_encryption_regenerate_system_keys (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Verwendung **Sp_pdw_database_encryption_regenerate_system_keys** drehen Sie das Zertifikat und Datenbank-Verschlüsselungsschlüssel für internen Datenbanken, die verschlüsselt werden, wenn TDE für die Anwendung aktiviert ist. einschließlich `tempdb`, zu verwenden. Dies ist nur erfolgreich, wenn TDE aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Die Prozedur hat keine Parameter.  
  
 Diese Prozedur sollte verwendet werden, wenn der Datenverkehr in der Einheit gering ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** feste Datenbankrolle oder **CONTROL SERVER** Berechtigung.  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel wird die Datenbank-Verschlüsselungsschlüssel erneut generiert.  
  
```tsql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_pdw_database_encryption aktiviert werden &#40; SQL Datawarehouse &#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [Sp_pdw_log_user_data_masking &#40; SQL Datawarehouse &#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
