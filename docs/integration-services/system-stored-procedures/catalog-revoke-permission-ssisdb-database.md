---
title: catalog.revoke_permission (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- revoke_permission stored procedure [Integration Services]
- catalog.revoke_permission stored procedure [Integration Services]
ms.assetid: 850b9c26-5c7c-47b9-a61c-5cf9bb5948cf
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2c71f38fd26b56cedc2b3309067b26b1a161966
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="catalogrevokepermission-ssisdb-database"></a>catalog.revoke_permission (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Widerruft eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.revoke_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argumente  
 [ @object_type = ] *object_type*  
 Der Typ des sicherungsfähigen Objekts. Die Typen von sicherungsfähigen Objekten umfassen Ordner (`1`), Projekt (`2`), Umgebung (`3`) und Vorgang (`4`). Das Argument *object_type* ist vom Typ **smallint***.*  
  
 [ @object_id = ] *object_id*  
 Der eindeutige Bezeichner (ID) des sicherungsfähigen Objekts. Das Argument *object_id* ist vom Typ **bigint**.  
  
 [ @principal_id = ] *principal_id*  
 Die ID des Prinzipals, dessen Berechtigung widerrufen werden soll. Das Argument *principal_id* ist vom Typ **int**.  
  
 [ @permission_type = ] *permission_type*  
 Art der Berechtigung. Das Argument *permission_type* ist vom Typ **smallint**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg)  
  
 1 („object_class“ ist ungültig)  
  
 2 („object_id“ ist nicht vorhanden)  
  
 3 („principal“ ist nicht vorhanden)  
  
 4 („permission“ ist ungültig)  
  
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
 Wenn „permission_type“ angegeben wird, entfernt die gespeicherte Prozedur die Berechtigung, die dem Prinzipal für das Objekt explizit zugewiesen wurde. Auch wenn keine solchen Instanzen vorhanden sind, gibt die Prozedur einen Erfolgscodewert (`0`) zurück. Wenn „permission_type“ ausgelassen wird, entfernt die gespeicherte Prozedur alle Berechtigungen des Prinzipals für das Objekt.  
  
> [!NOTE]  
>  Der Prinzipal verfügt möglicherweise immer noch über die angegebene Berechtigung für das Objekt, wenn der Prinzipal ein Mitglied einer Rolle ist, die über die angegebene Berechtigung verfügt.  
  
 Mit dieser gespeicherten Prozedur können Sie die in der folgenden Tabelle beschriebenen Typen von Berechtigungen widerrufen:  
  
|permission_type-Wert|Berechtigungsname|Berechtigungsbeschreibung|Anwendbare Objekttypen|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Ermöglicht es dem Prinzipal, Informationen zu lesen, die als Teil des Objekts angesehen werden, z. B. Eigenschaften. Ermöglicht es dem Prinzipal nicht, den Inhalt von anderen Objekten innerhalb des Objekts aufzuzählen oder zu lesen.|Ordner, Projekt, Umgebung, Vorgang|  
|`2`|MODIFY|Ermöglicht es dem Prinzipal, Informationen zu ändern, die als Teil des Objekts angesehen werden, z. B. Eigenschaften. Ermöglicht es dem Prinzipal nicht, andere Objekte innerhalb des Objekts zu ändern.|Ordner, Projekt, Umgebung, Vorgang|  
|`3`|Führen Sie|Ermöglicht es dem Prinzipal, alle Pakete im Projekt auszuführen.|Projekt|  
|`4`|MANAGE_PERMISSIONS|Ermöglicht es dem Prinzipal, den Objekten Berechtigungen zuzuweisen.|Ordner, Projekt, Umgebung, Vorgang|  
|`100`|CREATE_OBJECTS|Ermöglicht es dem Prinzipal, Objekte im Ordner zu erstellen.|Ordner|  
|`101`|READ_OBJECTS|Ermöglicht es dem Prinzipal, alle Objekte im Ordner zu lesen.|Ordner|  
|`102`|MODIFY_OBJECTS|Ermöglicht es dem Prinzipal, alle Objekte im Ordner zu ändern.|Ordner|  
|`103`|EXECUTE_OBJECTS|Ermöglicht es dem Prinzipal, alle Pakete aus allen Projekten im Ordner auszuführen.|Ordner|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Ermöglicht es dem Prinzipal, Berechtigungen für alle Objekte im Ordner zu verwalten.|Ordner|  
  
  
