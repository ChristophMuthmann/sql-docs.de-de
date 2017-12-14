---
title: catalog.disable_worker_agent (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3695d9a06c6de6e42409b7dba1e8e63e25925b73
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>catalog.disable_worker_agent (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Deaktivieren Sie einen Scale Out-Worker für einen Scale Out-Master, der mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog arbeitet.

## <a name="syntax"></a>Syntax

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>Argumente
[@WorkerAgentId =] *WorkerAgentId* Die Worker-Agent-ID für den Scale Out-Worker. Die *WorkerAgentId* ist **uniqueidentifier**.

## <a name="example"></a>Beispiel
In diesem Beispiel wird der Worker für horizontales Hochskalieren auf „MachineA“ deaktiviert.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  

## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin** 

## <a name="errors-and-warnings"></a>Fehler und Warnungen
Wenn die Worker-Agent-ID ungültig ist, gibt die gespeicherte Prozedur einen Fehler zurück.
