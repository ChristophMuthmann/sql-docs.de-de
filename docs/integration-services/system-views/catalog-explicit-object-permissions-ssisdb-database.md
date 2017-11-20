---
title: Catalog. explicit_object_permissions (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 49b09e0f-06e8-451f-b979-a0d91000bfe3
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ce92a61241cb70f5e1c6d1bab8db8264d6228bd2
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexplicitobjectpermissions-ssisdb-database"></a>catalog.explicit_object_permissions (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt nur die Berechtigungen an, die dem Benutzer explizit zugewiesen wurden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Der Typ des sicherungsfähigen Objekts. Typen sicherungsfähiger Objekte lauten Ordner (`1`), Projekt (`2`), Umgebung (`3`) und Vorgang (`4`).|  
|object_id|**bigint**|Der eindeutige Bezeichner (ID) oder der Primärschlüssel des sicherungsfähigen Objekts.|  
|principal_id|**int**|Die ID des Datenbankprinzipals.|  
|permission_type|**smallint**|Art der Berechtigung.|  
|is_deny|**bit**|Gibt an, ob die Berechtigung verweigert oder gewährt wurde. Wenn der Wert `1`ist, wurde die Berechtigung verweigert. Wenn der Wert `0`ist, wurde die Berechtigung nicht verweigert.|  
|grantor_id|**int**|Die ID des Prinzipals, der die Berechtigung gewährt hat.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht werden die in der folgenden Tabelle aufgeführten Berechtigungstypen angezeigt:  
  
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
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht bietet keine vollständige Sicht der Berechtigungen für den aktuellen Prinzipal. Der Benutzer muss außerdem überprüfen, ob der Prinzipal ein Mitglied von Rollen und Gruppen ist, denen Berechtigungen zugewiesen sind.  
  
  

