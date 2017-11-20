---
title: Catalog.set_worker_agent_property (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: c1caf4a71e5802968d9471711b8206a26f9c28d5
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>Catalog.set_worker_agent_property (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Setzt die Eigenschaft des eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale-Out-Worker.

## <a name="syntax"></a>Syntax

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>Argumente
[@WorkerAgentId =] *WorkerAgentId*  
Der Worker-Agent-ID der Skalierung Out Worker. Die *WorkerAgentId* ist **"uniqueidentifier"**.

[@PropertyName =] *PropertyName*  
Der Name der Eigenschaft. Die *PropertyName* ist **nvarchar(256)**.

[@PropertyValue =] *PropertyValue*  
Der Wert der Eigenschaft. Die *PropertyValue* ist **nvarchar(max)**.

## <a name="remarks"></a>Hinweise
Die gültigen Eigenschaftennamen sind **DisplayName**, **Beschreibung**, **Tags**.

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

-   Der Worker-Agent-ID ist ungültig.

-   Der Eigenschaftsname ist ungültig.

-   Der Eigenschaftswert ist ungültig.  

