---
title: Catalog. restore_project (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8adee525-579b-4d2f-b807-e2ecc07fb2e9
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 23074fc664591411666315036e3493e1b7b26134
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrestoreproject-ssisdb-database"></a>catalog.restore_project (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Stellt ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog in einer früheren Version.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
restore_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project _name  
    , [ @object_version_lsn = ] object_version_lsn  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, der das Projekt enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project _name =] *Project_name*  
 Der Name des Projekts. Der *project_name* ist **nvarchar(128)**.  
  
 [ @object_version_lsn =] *"object_version_lsn"*  
 Die Version des Projekts. Der *object_version_lsn* ist **bigint**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn der **project_name** gefunden wird, werden Projektdetails als *varbinary(MAX)* im Resultset zurückgegeben.  
  
 Wenn das Projekt nicht im angegebenen Ordner wiederhergestellt werden kann, wird**NO RESULT SET** zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Die Projektversion ist nicht vorhanden oder entspricht nicht dem Projektnamen.  
  
-   Das Projekt ist nicht vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Projekt wiederhergestellt wird, werden allen Parametern Standardwerte zugewiesen, und alle Umgebungsverweise bleiben unverändert. Die maximale Anzahl von Projektversionen, die im Katalog beibehalten werden, richtet sich nach der Katalogeigenschaft **MAX_VERSIONS_PER_PROJECT**, entsprechend der [Catalog_property](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) anzeigen.  
  
> [!WARNING]  
>  Umgebungsverweise sind möglicherweise nicht mehr gültig, nachdem ein Projekt wiederhergestellt wurde.  
  
  
