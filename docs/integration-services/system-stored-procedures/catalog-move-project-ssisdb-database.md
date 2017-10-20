---
title: Catalog. move_project (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ef3b0325-d8e9-472b-bf11-7d3efa6312ff
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5b091ccea1f733ebbf6e52308d17c7bdb7449cbe
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogmoveproject---ssisdb-database"></a>Catalog. move_project - SSISDB-Datenbank
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Verschiebt ein Projekt aus einem Ordner in einen anderen innerhalb der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.move_project [ @source_folder = ] source_folder  
    , [ @project_name = ] project_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>Argumente  
 [ @source_folder =] *Source_folder*  
 Der Name des Quellordners, in dem sich das Projekt vor dem Verschieben befindet. Der *source_folder* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts, das verschoben werden soll. Der *project_name* ist **nvarchar(128)**.  
  
 [ @destination_folder =] *Destination_folder*  
 Der Name des Zielordners, in dem sich das Projekt nach dem Verschieben befindet. Der *destination_folder* ist **nvarchar(128)**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für das Projekt, das verschoben werden soll, und CREATE_OBJECTS-Berechtigung für den Zielordner  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden Bedingungen beschrieben, die möglicherweise bewirken, dass diese gespeicherte Prozedur einen Fehler auslöst:  
  
-   Das Projekt ist nicht vorhanden.  
  
-   Der Quellordner nicht vorhanden.  
  
-   Der Zielordner ist nicht vorhanden, oder der Zielordner enthält bereits ein Projekt mit dem gleichen Namen.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Projekt von einem Quellordner in einen Zielordner verschoben wird, werden das Projekt im Quellordner und entsprechende Umgebungsverweise gelöscht. Im Zielordner werden ein identisches Projekt und Umgebungsverweise erstellt. Relative Umgebungsverweise verweisen nach dem Verschieben auf einen anderen Ordner. Absolute Verweise verweisen nach dem Verschieben auf den gleichen Ordner.  
  
> [!NOTE]  
>  Ein Projekt kann über relative oder absolute Umgebungsverweise verfügen. Relative Verweise verweisen mit dem Namen auf die Umgebung und erfordern, dass sich die Umgebung im gleichen Ordner wie das Projekt befindet. Absolute Verweise verweisen mit Name und Ordner auf die Umgebung, und sie verweisen auf Umgebungen, die sich in einem anderen Ordner als dem Ordner des Projekts befinden.  
  
  
