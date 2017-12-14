---
title: catalog.set_worker_agent_property (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1438d3a2cf200450791c085f501c49329d61154d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Legt die Eigenschaft eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Scale Out-Workers fest.

## <a name="syntax"></a>Syntax

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>Argumente
[@WorkerAgentId =] *WorkerAgentId*  
Die Worker-Agent-ID für den Scale Out-Worker. Das Argument *WorkerAgentId* ist vom Typ **uniqueidentifier**.

[@PropertyName =] *PropertyName*  
Der Name der Eigenschaft. Das Argument *PropertyName* ist vom Typ **nvarchar(256)**.

[@PropertyValue =] *PropertyValue*  
Der Wert der Eigenschaft. Das Argument *PropertyValue* ist vom Typ **nvarchar(max)**.

## <a name="remarks"></a>Hinweise
Die gültigen Eigenschaftennamen sind **DisplayName**, **Description**, **Tags**.

## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  

## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**

## <a name="errors-and-warnings"></a>Fehler und Warnungen
  In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen. 

-   Die Worker-Agent-ID ist ungültig.

-   Der Eigenschaftsname ist ungültig.

-   Der Eigenschaftswert ist ungültig.  
