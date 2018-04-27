---
title: catalog.set_environment_variable_value (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
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
ms.assetid: 1d493dad-9d9c-4f0a-87e2-20a2d4a35f99
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1647d1eb2adf731d9a7249a4871bb22709abaf56
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogsetenvironmentvariablevalue-ssisdb-database"></a>catalog.set_environment_variable_value (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Legt den Wert einer Umgebungsvariablen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name = ] *folder_name*  
 Der Name des Ordners, der die Umgebung enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 Der Name der Umgebung. Der *environment_name* ist **nvarchar(128)**.  
  
 [ @variable _name = ] *variable _name*  
 Der Name der Umgebungsvariablen. Der *variable _name* ist **nvarchar(128)**.  
  
 [ @value = ] *value*  
 Der Wert der Umgebungsvariablen. Der *value* ist **sql_variant**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für die Umgebung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der Ordnername ist ungültig.  
  
-   Der Umgebungsname ist ungültig.  
  
-   Der Umgebungsvariablenname ist ungültig.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
  
