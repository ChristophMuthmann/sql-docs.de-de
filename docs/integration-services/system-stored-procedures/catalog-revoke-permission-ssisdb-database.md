---
title: Catalog. revoke_permission (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- revoke_permission stored procedure [Integration Services]
- catalog.revoke_permission stored procedure [Integration Services]
ms.assetid: 850b9c26-5c7c-47b9-a61c-5cf9bb5948cf
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f058368bdd39b31a569d8810cccfc4d03d9f875e
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrevokepermission-ssisdb-database"></a>catalog.revoke_permission (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Widerruft eine Berechtigung für ein sicherungsfähiges Objekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.revoke_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumente  
 [ @object_type =] *Object_type*  
 Der Typ des sicherungsfähigen Objekts. Typen sicherungsfähiger Objekte lauten Ordner (`1`), Projekt (`2`), Umgebung (`3`), und Vorgang (`4`). Die *Object_type* ist **"smallint"***.*  
  
 [ @object_id =] *Object_id*  
 Die eindeutige Identitifier (ID) des sicherungsfähigen Objekts. Die *Object_id* ist **"bigint"**.  
  
 [ @principal_id =] *Principal_id*  
 Die ID des Prinzipals, dessen Berechtigung widerrufen werden soll. Die *Principal_id* ist **Int**.  
  
 [ @permission_type =] *Permission_type*  
 Art der Berechtigung. Die *Permission_type* ist **"smallint"**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg)  
  
 1 (Object_class ist nicht gültig.)  
  
 2 (Object_id ist nicht vorhanden)  
  
 3 (Prinzipal ist nicht vorhanden)  
  
 4 (Berechtigung ist nicht gültig.)  
  
 5 (anderer Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   ASSIGN_PERMISSIONS-Berechtigungen für das Objekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="remarks"></a>Hinweise  
 Wenn Permission_type angegeben wird, entfernt die gespeicherte Prozedur die Berechtigung, die dem Prinzipal für das Objekt explizit zugewiesen ist. Auch wenn keine solchen Instanzen vorhanden sind, gibt die Prozedur einen Erfolgscodewert (`0`) zurück. Wenn Permission_type weggelassen wird, entfernt die gespeicherte Prozedur alle Berechtigungen des Prinzipals für das Objekt an.  
  
> [!NOTE]  
>  Der Prinzipal verfügt möglicherweise immer noch über die angegebene Berechtigung für das Objekt, wenn der Prinzipal ein Mitglied einer Rolle ist, die über die angegebene Berechtigung verfügt.  
  
 Mit dieser gespeicherten Prozedur können Sie die in der folgenden Tabelle beschriebenen Typen von Berechtigungen widerrufen:  
  
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
  
  

