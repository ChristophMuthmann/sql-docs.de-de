---
title: catalog.grant_permission (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
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
- grant_permission stored procedure [Integration Services]
- catalog.grant_permission stored procedure [Integration Services]
ms.assetid: e72cfd52-de66-45e9-98b9-b8580ac7b956
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7c079453409e0af538aaeb2c82f6596e05b7d49
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="cataloggrantpermission-ssisdb-database"></a>catalog.grant_permission (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gewährt eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.grant_permission [ @object_type = ] object_type  
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
 Die ID des Prinzipals, dem eine Berechtigung gewährt werden soll. Das Argument *principal_id* ist vom Typ **int**.  
  
 [ @permission_type = ] *permission_type*  
 Der Typ der zu gewährenden Berechtigung. Das Argument *permission_type* ist vom Typ **smallint**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg)  
  
 1 („object_class“ ist ungültig)  
  
 2 („object_id“ ist nicht vorhanden)  
  
 3 („principal“ ist nicht vorhanden)  
  
 4 („permission“ ist ungültig)  
  
 5 (anderer Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   ASSIGN_PERMISSIONS-Berechtigungen für das Objekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  

Dieses Verfahren kann nicht durch Anmeldevorgänge aufgerufen werden, die von SQL Server authentifiziert wurden. Es kann nicht durch die SA-Anmeldung aufgerufen werden.
  
## <a name="remarks"></a>Hinweise  
 Mit dieser gespeicherten Prozedur können Sie die in der folgenden Tabelle beschriebenen Typen von Berechtigungen gewähren:  
  
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
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 Entsprechende Fehler und Meldungen finden Sie im Abschnitt "Rückgabecodewerte".  
  
  
