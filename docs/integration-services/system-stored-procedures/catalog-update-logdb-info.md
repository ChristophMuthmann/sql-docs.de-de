---
title: Catalog.update_logdb_info (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
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
ms.openlocfilehash: 5985699fc8afbfe2206d2e4da383794e779bde59
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
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
 
