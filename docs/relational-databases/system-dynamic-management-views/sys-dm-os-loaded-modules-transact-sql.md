---
title: Sys. dm_os_loaded_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_loaded_modules
- dm_os_loaded_modules
- sys.dm_os_loaded_modules_TSQL
- dm_os_loaded_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_loaded_modules dynamic management view
ms.assetid: 56c7743a-b568-4943-bd3b-73c57d9d641c
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 29e91f1859eb1dabe8bfa7df42acf594c021679d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosloadedmodules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt für jedes in den Serveradressbereich geladene Modul eine Zeile zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_loaded_modules**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary(8)**|Adresse des Moduls im Prozess.|  
|**file_version**|**varchar(23)**|Version der Datei. Hält das folgende Format ein:<br /><br /> x.x:x.x|  
|**product_version**|**varchar(23)**|Version des Produkts. Hält das folgende Format ein:<br /><br /> x.x:x.x|  
|**debug**|**bit**|1 = Modul ist eine Debugversion des geladenen Moduls.|  
|**gepatcht**|**bit**|1 = Modul wurde gepatcht.|  
|**prerelease**|**bit**|1 = Modul ist eine Vorabversion des geladenen Moduls.|  
|**private_build**|**bit**|1 = Modul ist ein privater Build des geladenen Moduls.|  
|**special_build**|**bit**|1 = Modul ist ein spezieller Build des geladenen Moduls.|  
|**Sprache**|**int**|Sprache der Versionsinformationen des Moduls.|  
|**Unternehmensportal**|**nvarchar(256)**|Name des Unternehmens, von dem das Modul erstellt wurde.|  
|**description**|**nvarchar(256)**|Beschreibung des Moduls.|  
|**name**|**nvarchar(255)**|Name des Moduls. Schließt den vollständigen Pfad des Moduls ein.|  
|**pdw_node_id**|**int**|**Gilt für:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
