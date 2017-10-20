---
title: Catalog. rename_environment (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: c73d7452-31c5-4f4e-afcc-e9eca760c826
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 504d3ca0f18c9ea11105ebb575d2f5db449f91e4
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenameenvironment-ssisdb-database"></a>catalog.rename_environment (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Benennt eine Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog um.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
rename_environment [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @new_environment_name= ] new_environment_name  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, der die Umgebung enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @environment_name =] *Environment_name*  
 Der ursprüngliche Name der Umgebung. Der *environment_name* ist **nvarchar(128)**.  
  
 [ @new_environment_name =] *New_environment_name*  
 Der neue Name der Umgebung. Der *new_environment_name* ist **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   MODIFY-Berechtigung für die Umgebung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Der ursprüngliche Umgebungsname ist ungültig.  
  
-   Der neue Name wurde bereits für eine vorhandene Umgebung verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Umgebungsverweise aus Projekten werden nicht automatisch aktualisiert, wenn Sie die Umgebung umbenennen. Umgebungsverweise müssen entsprechend aktualisiert werden. Diese gespeicherte Prozedur wird auch dann erfolgreich ausgeführt, wenn Umgebungsverweise durch das Ändern des Umgebungsnamens beschädigt werden. Nach Abschluss dieser gespeicherten Prozedur müssen Umgebungsverweise aktualisiert werden.  
  
> [!NOTE]  
>  Wenn ein Umgebungsverweis ungültig ist, schlagen Überprüfung und Ausführung der entsprechenden Pakete fehl, von denen diese Verweise verwendet werden.  
  
  
