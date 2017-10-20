---
title: Catalog. delete_project (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: abc0280a693be8e0f9fa9b3ec997c1d38d96ed54
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeleteproject-ssisdb-database"></a>catalog.delete_project (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Löscht ein vorhandenes Projekt aus einem Ordner in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name =] *Ordnername*  
 Der Name des Ordners, der das Projekt enthält. *folder_name* ist **nvarchar(128)**  
  
 [ @project_name =] *Project_name*  
 Der Name des Projekts, das gelöscht werden soll. *project_name* ist **nvarchar(128)**  
  
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
 Die folgende Liste beschreibt einige Bedingungen, die möglicherweise die Delete_project gespeicherte Prozedur einen Fehler auslöst:  
  
-   Das Projekt ist nicht vorhanden.  
  
-   Der Ordner ist nicht vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Alle Objekte und Umgebungsverweise des entsprechenden Projekts werden zusammen mit dem Projekt gelöscht. Die Versionen des Projekts und die relevanten Vorgangsdatensätze werden jedoch bis zur nächsten Ausführung des Vorgangscleanupauftrags beibehalten.  
  
  
