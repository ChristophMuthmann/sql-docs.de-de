---
title: Catalog.worker_agents (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d56af0ab150255c53746898a638a32112938755c
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="catalogworkeragents-ssisdb-database"></a>Catalog.worker_agents (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Zeigt die Informationen für die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale-Out-Worker.

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Der Worker-Agent-ID der Skalierung Out Worker.|
|isEnabled|**bit**|Gibt an, ob die Skala Out Worker aktiviert ist.|
|DisplayName|**nvarchar(256)**|Der Anzeigename des Scale-Out-Worker.|
|Description|**nvarchar(256)**|Die Beschreibung des Scale-Out-Worker.|
|MachineName|**nvarchar(256)**|Der Name des Computers, für den Scale-Out-Worker werden soll.|
|Tags|**nvarchar(max)**|Die Tags Scale-Out-Worker.|
|UserAccount|**nvarchar(256)**|Das Benutzerkonto, das Scale-Out-Worker-Dienst ausgeführt wird.|
|LastOnlineTime|**DateTimeOffset(7)**|Zeitpunkt der letzten, die die Skala Out Worker online ist.|

## <a name="remarks"></a>Hinweise
In dieser Ansicht wird eine Zeile für jede Scale Out Worker Herstellen einer Verbindung mit der Skala Out Master arbeiten mit den SSISDB-Katalog angezeigt.

## <a name="permissions"></a>Berechtigungen
Diese Sicht erfordert eine der folgenden Berechtigungen:

- Mitgliedschaft in der Datenbankrolle **ssis_admin**

- Die Mitgliedschaft in der **Ssis_cluster_executor** -Datenbankrolle

- Mitgliedschaft in der Serverrolle **sysadmin**

