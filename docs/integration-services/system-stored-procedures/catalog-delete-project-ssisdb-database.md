---
title: catalog.delete_project (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f3431445-8dd2-443b-813e-b99db893977e
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c09d08c3b115a3d5171d368aba7373240458cd48
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogdeleteproject-ssisdb-database"></a>catalog.delete_project (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Löscht ein vorhandenes Projekt aus einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name = ] *folder_name*  
 Der Name des Ordners, der das Projekt enthält. *folder_name* ist **nvarchar(128)**  
  
 [ @project_name = ] *project_name*  
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
 In der folgenden Liste werden Bedingungen beschrieben, die möglicherweise bewirken, dass die gespeicherte Prozedur „delete_project“ einen Fehler auslöst:  
  
-   Das Projekt ist nicht vorhanden.  
  
-   Der Ordner ist nicht vorhanden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Alle Objekte und Umgebungsverweise des entsprechenden Projekts werden zusammen mit dem Projekt gelöscht. Die Versionen des Projekts und die relevanten Vorgangsdatensätze werden jedoch bis zur nächsten Ausführung des Vorgangscleanupauftrags beibehalten.  
  
  
