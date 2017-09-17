---
title: Catalog.set_worker_agent_property (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d0476bbb67cff44a05aed1441a31d679882b4cb3
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>Catalog.set_worker_agent_property (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Setzt die Eigenschaft des eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale-Out-Worker.

## <a name="syntax"></a>Syntax

```tsql
set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId, [ @PropertyName = ] PropertyName, [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>Argumente
[ @WorkerAgentId =] *WorkerAgentId*  
Die Worker-Agent-Id des Scale-Out-Worker. Die *WorkerAgentId* ist **"uniqueidentifier"**.

[ @PropertyName =] *PropertyName*  
Der Name der Eigenschaft. Die *PropertyName* ist **nvarchar(256)**.

[ @PropertyValue =] *PropertyValue*  
Der Wert der Eigenschaft. Die *PropertyValue* ist **nvarchar(max)**.

## <a name="remarks"></a>Hinweise
Sind die gültigen Namen für die gesammelten **DisplayName**, **Beschreibung**, **Tags**.

## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  

## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**

## <a name="erros-and-warnings"></a>Fehler und Warnungen
  In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen. 

-   Der Worker-Agent-Id ist ungültig.

-   Der Eigenschaftsname ist ungültig.

-   Der Eigenschaftswert ist nicht Vilid.  
