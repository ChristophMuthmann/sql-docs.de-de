---
title: Catalog.enable_worker_agent (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c6e5266b-c32d-49ff-aa69-f09664009fb4
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: b348939327efbacbb612e28c4c30fbb2d7cc0a17
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="catalogenableworkeragent-ssisdb-database"></a>Catalog.enable_worker_agent (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Aktivieren Sie eine Skalierung Out Worker für Scale Out Master arbeiten mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.

## <a name="syntax"></a>Syntax

```tsql
enable_worker_agent [@WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>Argumente
[ @WorkerAgentId =] *WorkerAgentId* die Worker-Agent-Id des Scale-Out-Worker. Die *WorkerAgentId* ist **"uniqueidentifier"**.

## <a name="example"></a>Beispiel
In diesem Beispiel wird Worker für horizontales Hochskalieren auf „MachineA“ aktiviert.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
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
Die gespeicherte Prozedur gibt einen Fehler zurück, wenn die Worker-Agent-ID ungültig ist.

