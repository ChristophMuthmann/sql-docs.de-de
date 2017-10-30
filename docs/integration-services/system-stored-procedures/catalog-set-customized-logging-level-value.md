---
title: Catalog.set_customized_logging_level_value | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 75ef405fe4550e81ec2d5178a1d3242d405755af
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedlogginglevelvalue"></a>Catalog.set_customized_logging_level_value
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ändert die Statistiken oder von einer vorhandenen benutzerdefinierten Protokolliergrad protokollierten Ereignisse. Weitere Informationen über benutzerdefinierte Protokolliergrade, finden Sie unter [Integration Services &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumente  
 [ @level_name =] *Ebenenname*  
 Der Name eines vorhandenen benutzerdefinierten Protokolliergrads.  
  
 Die *Ebenenname* ist **vom Datentyp nvarchar(128)**.  
  
 [ @property_name =] *Property_name*  
 Der Name des zu ändernden Eigenschaft. Gültige Werte sind **Profil** und **Ereignisse**.  
  
 Der *property_name* ist **nvarchar(128)**.  
  
 [ @property_value =] *Property_value*  
 Der neue Wert für die angegebene Eigenschaft des angegebenen benutzerdefinierten Protokolliergrads.  
  
 Eine Liste der gültigen Werte für das Profil und Ereignisse, finden Sie unter [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).  
  
 Die *Property_value* ist ein **"bigint"**.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="return-codes"></a>Rückgabecodes  
 0 (Erfolg)  
  
 Wenn die gespeicherte Prozedur fehlschlägt, wird ein Fehler ausgelöst.  
  
## <a name="result-set"></a>Resultset  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt Bedingungen, unter denen die gespeicherte Prozedur fehlschlägt.  
  
-   Der Benutzer besitzt nicht die erforderlichen Berechtigungen.  
  
  

