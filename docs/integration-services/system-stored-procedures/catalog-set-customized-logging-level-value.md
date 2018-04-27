---
title: catalog.set_customized_logging_level_value | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfbd94cfa574c224f0f45d1eeb433107d43380da
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogsetcustomizedlogginglevelvalue"></a>catalog.set_customized_logging_level_value
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ändert die Statistiken oder Ereignisse, die von einem vorhandenen benutzerdefinierten Protokolliergrad protokolliert werden. Weitere Informationen zu benutzerdefinierten Protokolliergraden finden Sie unter [Integration Services &#40;SSIS&#41; Logging (SSIS-Protokollierung [SQL Server Integration Services])](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumente  
 [ @level_name = ] *level_name*  
 Der Name für einen vorhandenen benutzerdefinierten Protokolliergrad.  
  
 Das Argument *level_name* ist vom Typ **nvarchar(128)**.  
  
 [ @property_name = ] *property_name*  
 Der Name der zu ändernden Eigenschaft. Gültige Werte sind **PROFILE** und **EVENTS**.  
  
 Der *property_name* ist **nvarchar(128)**.  
  
 [ @property_value = ] *property_value*  
 Der neue Wert für die angegebene Eigenschaft des angegebenen benutzerdefinierten Protokolliergrads.  
  
 Eine Liste der gültigen Werte für PROFILE und EVENTS finden Sie unter [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).  
  
 Das Argument *property_value* ist vom Typ **bigint**.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Der Benutzer verfügt nicht über die erforderlichen Berechtigungen.  
  
  
