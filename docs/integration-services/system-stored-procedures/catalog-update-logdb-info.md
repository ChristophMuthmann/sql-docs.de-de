---
title: Catalog.update_logdb_info (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: abc72a63dafe96b98e954b8f4d01d9c320abc364
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="catalogupdatelogdbinfo-ssisdb-database"></a>Catalog.update_logdb_info (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Aktualisieren Sie die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Scale Out-Protokollinformationen.

## <a name="syntax"></a>Syntax

```sql
catalog.update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>Argumente
[ @server_name = ] *server_name*  
 Die für die Scale Out-Protokollierung verwendete SQL Server-Instanz. Der *server_name* ist **nvarchar**.  

 [ @connection_string = ] *connection_string*  
 Die Verbindungszeichenfolge, die für Scale Out-Protokollierung verwendet wird. Der *connection_string* ist **nvarchar**.

 ## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 InclusionThresholdSetting  

## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
   
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
 
