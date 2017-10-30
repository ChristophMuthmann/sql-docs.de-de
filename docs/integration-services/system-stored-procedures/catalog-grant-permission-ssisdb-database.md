---
title: Catalog. grant_permission (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- grant_permission stored procedure [Integration Services]
- catalog.grant_permission stored procedure [Integration Services]
ms.assetid: e72cfd52-de66-45e9-98b9-b8580ac7b956
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 5f9bb38521631bcc60d39fba747f17b86183545d
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="cataloggrantpermission-ssisdb-database"></a>catalog.grant_permission (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gewährt eine Berechtigung für ein sicherungsfähiges Objekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.grant_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumente  
 [ @object_type =] *Object_type*  
 Der Typ des sicherungsfähigen Objekts. Typen sicherungsfähiger Objekte lauten Ordner (`1`), Projekt (`2`), Umgebung (`3`), und Vorgang (`4`). Die *Object_type* ist **"smallint"***.*  
  
 [ @object_id =] *Object_id*  
 Der eindeutige Bezeichner (ID) des sicherungsfähigen Objekts. Die *Object_id* ist **"bigint"**.  
  
 [ @principal_id =] *Principal_id*  
 Die ID des Prinzipals, dem eine Berechtigung gewährt werden soll. Die *Principal_id* ist **Int**.  
  
 [ @permission_type =] *Permission_type*  
 Der Typ der zu gewährenden Berechtigung. Die *Permission_type* ist **"smallint"**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg)  
  
 1 (Object_class ist ungültig.)  
  
 2 (Object_id ist nicht vorhanden)  
  
 3 (Prinzipal ist nicht vorhanden)  
  
 4 (Berechtigung ist ungültig.)  
  
 5 (anderer Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   ASSIGN_PERMISSIONS-Berechtigungen für das Objekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  

Dieses Verfahren kann nicht von Anmeldungen, die von SQL Server authentifiziert wurden, nicht aufgerufen werden. Er kann nicht von der Anmeldenamens "sa" aufgerufen werden.
  
## <a name="remarks"></a>Hinweise  
 Mit dieser gespeicherten Prozedur können Sie die in der folgenden Tabelle beschriebenen Typen von Berechtigungen gewähren:  
  
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
 Entsprechende Fehler und Meldungen finden Sie im Abschnitt "Rückgabecodewerte".  
  
  

