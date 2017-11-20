---
title: Catalog. deny_permission (SSISDB-Datenbank) | Microsoft Docs
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
ms.assetid: de310bac-2ddc-4ef9-8783-43dcb02a94f1
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 689a59e92286881fa3be7ee3754a786ccb54ae6c
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdenypermission-ssisdb-database"></a>catalog.deny_permission (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Verweigert eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.deny_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumente  
 [ @object_type =] *Object_type*  
 Der Typ des sicherungsfähigen Objekts. Typen sicherungsfähiger Objekte lauten Ordner (`1`), Projekt (`2`), Umgebung (`3`), und Vorgang (`4`). Die *Object_type* ist **"smallint"***.*  
  
 [ @object_id =] *Object_id*  
 Der eindeutige Bezeichner (ID) oder der Primärschlüssel des sicherungsfähigen Objekts. Die *Object_id* ist **"bigint"**.  
  
 [ @principal_id =] *Principal_id*  
 Die ID des Prinzipals, der verweigert werden soll. Die *Principal_id* ist **Int**.  
  
 [ @permission_type =] *Permission_type*  
 Der Typ der Berechtigung, die verweigert werden soll. Die *Permission_type* ist **"smallint"**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg)  
  
 1 (Object_class ist nicht gültig.)  
  
 2 (Object_id ist nicht vorhanden)  
  
 3 (Prinzipal ist nicht vorhanden)  
  
 4 (Berechtigung ist nicht gültig.)  
  
 5 (anderer Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   MANAGE_PERMISSIONS-Berechtigung für das Objekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="remarks"></a>Hinweise  
 Mit dieser gespeicherten Prozedur können Sie die in der folgenden Tabelle beschriebenen Typen von Berechtigungen verweigern:  
  
|permission_type-Wert|Berechtigungsname|Berechtigungsbeschreibung|Anwendbare Objekttypen|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Ermöglicht es dem Prinzipal, Informationen zu lesen, die als Teil des Objekts angesehen werden, z. B. Eigenschaften. Ermöglicht es dem Prinzipal nicht, den Inhalt von anderen Objekten innerhalb des Objekts aufzuzählen oder zu lesen.|Ordner, Projekt, Umgebung, Vorgang|  
|`2`|MODIFY|Ermöglicht es dem Prinzipal, Informationen zu ändern, die als Teil des Objekts angesehen werden, z. B. Eigenschaften. Ermöglicht es dem Prinzipal nicht, andere Objekte innerhalb des Objekts zu ändern.|Ordner, Projekt, Umgebung, Vorgang|  
|`3`|EXECUTE|Ermöglicht es dem Prinzipal, alle Pakete im Projekt auszuführen.|Projekt|  
|`4`|MANAGE_PERMISSIONS|Ermöglicht es dem Prinzipal, den Objekten Berechtigungen zuzuweisen.|Ordner, Projekt, Umgebung, Vorgang|  
|`100`|CREATE_OBJECTS|Ermöglicht es dem Prinzipal, Objekte im Ordner zu erstellen.|Ordner|  
|`101`|READ_OBJECTS|Ermöglicht es dem Prinzipal, alle Objekte im Ordner zu lesen.|Ordner|  
|`102`|MODIFY_OBJECTS|Ermöglicht es dem Prinzipal, alle Objekte im Ordner zu ändern.|Ordner|  
|`103`|EXECUTE_OBJECTS|Ermöglicht es dem Prinzipal, alle Pakete aus allen Projekten im Ordner auszuführen.|Ordner|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Ermöglicht es dem Prinzipal, Berechtigungen für alle Objekte im Ordner zu verwalten.|Ordner|  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Wenn Permission_type angegeben wird, verweigert die Prozedur die angegebene Berechtigung, die dem angegebenen Prinzipal für das angegebene Objekt explizit zugewiesen ist. Auch wenn keine solchen Instanzen vorhanden sind, gibt die Prozedur dennoch einen Erfolgscodewert (`0`) zurück.  
  
-   Wenn Permission_type weggelassen wird, verweigert die Prozedur alle Berechtigungen für den angegebenen Prinzipal mit dem angegebenen Objekt.  
  
  

