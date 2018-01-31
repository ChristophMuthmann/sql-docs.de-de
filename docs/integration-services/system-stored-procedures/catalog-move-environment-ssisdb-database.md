---
title: catalog.move_environment (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: b3fb5242-3c4c-4a87-b3e5-beb22fbab053
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd8598e526761f51e361fcc7c3330bbe3c9a470f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="catalogmoveenvironment-ssisdb-database"></a>catalog.move_environment (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Verschiebt eine Umgebung von einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog in einen anderen.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.move_environment [ @source_folder = ] source_folder  
    , [ @environment_name = ] environment_name  
    , [ @destination_folder = ] destination_folder  
```  
  
## <a name="arguments"></a>Argumente  
 [ @source_folder = ] *source_folder*  
 Der Name des Quellordners, in dem sich die Umgebung vor dem Verschieben befindet. Der *source_folder* ist **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 Der Name der Umgebung, die verschoben werden soll. Der *environment_name* ist **nvarchar(128)**.  
  
 [ @destination_folder = ] *destination_folder*  
 Der Name des Zielordners, in dem sich die Umgebung nach dem Verschieben befindet. Der *destination_folder* ist **nvarchar(128)**.  
  
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
  
-   Die Umgebung ist im Quellordner nicht vorhanden.  
  
-   Für den Zielordner ist bereits eine Umgebung mit dem gleichen Namen vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Remarks  
 Umgebungsverweise aus Projekten werden nicht während des Verschiebens der Umgebung entsprechend angepasst. Umgebungsverweise müssen entsprechend aktualisiert werden. Diese gespeicherte Prozedur wird auch dann erfolgreich ausgeführt, wenn Umgebungsverweise durch das Verschieben einer Umgebung beschädigt werden. Nach Abschluss dieser gespeicherten Prozedur müssen Umgebungsverweise aktualisiert werden.  
  
> [!NOTE]  
>  Ein Projekt kann über relative oder absolute Umgebungsverweise verfügen. Relative Verweise verweisen mit dem Namen auf die Umgebung und erfordern, dass sich die Umgebung im gleichen Ordner wie das Projekt befindet. Absolute Verweise verweisen mit Name und Ordner auf die Umgebung, und sie verweisen auf Umgebungen, die sich in einem anderen Ordner als dem Ordner des Projekts befinden.  
  
  
