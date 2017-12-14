---
title: catalog.folders (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a439659dd93bdcd4d6c627782de8772adfe6466
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|id|**bigint**|Der eindeutige Bezeichner des Ordners.|  
|name|**sysname(nvarchar(128))**|Der Name des Ordners, der innerhalb des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalogs eindeutig ist.|  
|Beschreibung|**nvarchar(1024)**|Die Beschreibung des Ordners.|  
|created_by_sid|**varbinary(85)**|Die Sicherheits-ID (SID) des Benutzers, der den Ordner erstellt hat|  
|created_by_name|**nvarchar(128)**|Der Name des Benutzers, der den Ordner erstellt hat.|  
|created_time|**datetimeoffset(7)**|Datum und Uhrzeit der Ordnererstellung.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jeden Ordner im Katalog angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für den Ordner  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  
