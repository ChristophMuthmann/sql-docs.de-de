---
title: Catalog.deploy_packages | Microsoft Docs
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
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1839430dd7fb83ab16c4de46011819e3ce28e835
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeploypackages"></a>Catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Stellt ein oder mehrere Pakete in einen Ordner in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog hinzu oder aktualisiert ein vorhandenes Paket, das zuvor bereitgestellt wurde.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts im Ordner "". Der *project_name* ist **nvarchar(128)**.  
  
 [ @packages_table =] *Packages_table*  
 Die binären Inhalte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (.dtsx)-Dateien verpacken. Die *Packages_table* ist **[Catalog]. [ Package_Table_Type]**  
  
 [ @operation_id =] *Operation_id*  
 Gibt den eindeutigen Bezeichner für den Bereitstellungsvorgang zurück. Der *operation_id* ist **bigint**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   CREATE_OBJECTS-Berechtigungen für das Projekt oder die MODIFY-Berechtigung für das Paket zum Aktualisieren eines Pakets.  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden Bedingungen beschrieben, die möglicherweise bewirken, dass diese gespeicherte Prozedur einen Fehler auslöst:  
  
-   Ein Parameter verweist auf ein Objekt, das nicht vorhanden ist, ein Parameter versucht, ein Objekt zu erstellen, die bereits vorhanden ist oder ein Parameter in anderer Weise ungültig ist.  
  
-   Der Benutzer verfügt nicht über ausreichende Berechtigungen  
  
  

