---
title: Catalog. clear_object_parameter_value (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: dcbbb714-a051-4805-9e2b-2c2fb647c890
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d0d89081a31341a8d813d9985940c0e3ce0160a
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogclearobjectparametervalue-ssisdb-database"></a>catalog.clear_object_parameter_value (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Löscht den Wert eines Parameters für eine vorhandene [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Projekt oder Paket, das auf dem Server gespeichert ist.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, der das Projekt enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts. Der *project_name* ist **nvarchar(128)**.  
  
 [ @object_type =] *Object_type*  
 Der Typ des Objekts. Gültige Werte sind `20` für ein Projekt und `30` für ein Paket. Der *object_type* ist **smallInt**.  
  
 [ @ object _name = ] *object _name*  
 Der Name des Pakets. Der *object _name* ist **nvarchar(260)**.  
  
 [ @parameter_ Name =] *Parameter_name*  
 Der Name des Parameters. Der *parameter_ name* ist **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Die folgende Liste beschreibt einige Bedingungen, die möglicherweise die Clear_object_parameter gespeicherte Prozedur einen Fehler auslöst:  
  
-   Es wurde ein ungültiger Objekttyp angegeben, oder der Objektname wurde nicht im Projekt gefunden.  
  
-   Das Projekt ist nicht vorhanden, auf das Projekt kann nicht zugegriffen werden, oder der Projektname ist ungültig.  
  
-   Es wurde ein ungültiger Parametername angegeben.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
  

