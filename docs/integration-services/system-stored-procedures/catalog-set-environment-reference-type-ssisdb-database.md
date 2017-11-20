---
title: Catalog. set_environment_reference_type (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e83d9979ee4736528efb4851848ea3eac717fab8
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Legt den Verweistyp fest und den Umgebungsnamen verknüpft sind mit einem vorhandenen umgebungsverweis für ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @reference_id =] *Reference_id*  
 Der eindeutige Bezeichner des Umgebungsverweises, der aktualisiert werden soll. Der *reference_id* ist **bigint**.  
  
 [ @reference_type =] *Reference_type*  
 Gibt an, ob sich die Umgebung im gleichen Ordner wie das Projekt (relativer Verweis) oder in einem anderen Ordner (absoluter Verweis) befinden kann. Verwenden Sie den Wert `R` , um einen relativen Verweis anzugeben. Verwenden Sie den Wert `A` , um einen absoluten Verweis anzugeben. Der *reference_type* ist **char(1)**.  
  
 [ @environment_folder_name =] *Environment_folder_name*  
 Der Ordner, in dem sich die Umgebung befindet. Dieser Wert ist für absolute Verweise erforderlich. Der *environment_folder_name* ist **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für das Projekt und READ-Berechtigung für die Umgebung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Ordnername, der Umgebungsname oder die Verweis-ID ist ungültig.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Im `A` -Parameter wird mit dem Zeichen *A* ein absoluter Verweis angegeben, jedoch wurde im *environment_folder_name* -Parameter nicht der Name des Ordners angegeben.  
  
## <a name="remarks"></a>Hinweise  
 Ein Projekt kann über relative oder absolute Umgebungsverweise verfügen. Relative Verweise verweisen mit dem Namen auf die Umgebung und erfordern, dass sich diese im gleichen Ordner wie das Projekt befindet. Absolute Verweise verweisen mit Name und Ordner auf die Umgebung und verweisen möglicherweise auf Umgebungen, die sich in einem anderen Ordner als das Projekt befinden. Ein Projekt kann auf mehrere Umgebungen verweisen.  
  
> [!IMPORTANT]  
>  Wenn ein relativer Verweis angegeben wird, wird der *environment_folder_name* -Parameterwert nicht verwendet, und der Umgebungsordnername wird automatisch auf **NULL**festgelegt. Wenn ein absoluter Verweis angegeben wird, muss der Umgebungsordnername im *environment_folder_name* -Parameter angegeben werden.  
  
  

