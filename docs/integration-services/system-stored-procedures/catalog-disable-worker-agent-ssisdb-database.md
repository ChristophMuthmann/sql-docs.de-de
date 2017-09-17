---
title: Catalog.disable_worker_agent (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: aab83dd2f179c8e6b90ad9ff7a212597a51038de
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>Catalog.disable_worker_agent (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Deaktivieren Sie eine Skala Out Worker für Skalierung Out Master arbeiten mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.

## <a name="syntax"></a>Syntax

```tsql
disable_worker_agent [@WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>Argumente
[ @WorkerAgentId =] *WorkerAgentId* die Worker-Agent-Id des Scale-Out-Worker. Die *WorkerAgentId* ist **"uniqueidentifier"**.

## <a name="example"></a>Beispiel
In diesem Beispiel wird die Skalierung Out Worker auf ComputerA deaktiviert.
```tsql
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
Die gespeicherte Prozedur gibt einen Fehler zurück, wenn die Worker-Agent-ID ungültig ist.

