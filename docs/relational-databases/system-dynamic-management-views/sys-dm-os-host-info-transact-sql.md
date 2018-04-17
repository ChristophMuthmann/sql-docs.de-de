---
title: Sys.dm_os_host_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e8e36375f534a187c749bbd4217fddd0a98f8fb9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmoshostinfo-transact-sql"></a>Sys.dm_os_host_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gibt eine Zeile, in dem Informationen zur Betriebssystemversion angezeigt.  
  
|Spaltenname |Datentyp |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |Der Typ des Betriebssystems: Windows- oder Linux |
|**host_distribution** |**nvarchar(256)** |Beschreibung des Betriebssystems. |
|**host_release**|**nvarchar(256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Betriebssystem-Version (Versionsnummer). Eine Liste der Werte mit Beschreibungen finden Sie unter [Betriebssystemversion (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx). <br> Für Linux zurückgegeben eine leere Zeichenfolge. |  
|**host_service_pack_level**|**nvarchar(256)**|Service Pack-Ebene des Windows-Betriebssystems. <br> Für Linux zurückgegeben eine leere Zeichenfolge. |  
|**host_sku**|**int**|Windows-SKU-ID (Stock Keeping Unit). Eine Liste mit SKU-IDs und Beschreibungen finden Sie unter [Funktion "GetProductInfo"](http://msdn.microsoft.com/library/ms724358.aspx). Lässt NULL-Werte zu. <br> Für Linux wird NULL zurückgegeben. |  
|**os_language_version**|**int**|Windows-Gebietsschemabezeichner (LCID) des Betriebssystems. Eine Liste mit LCID-Werten und Beschreibungen finden Sie unter [Von Microsoft zugewiesene Gebietsschemabezeichner (LCIDs)](http://go.microsoft.com/fwlink/?LinkId=208080). Lässt keine NULL-Werte zu.|  

## <a name="remarks"></a>Hinweise  
Diese Ansicht ist ähnlich wie [dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), Hinzufügen von Spalten, die Windows- und Linux Argumentlisten zur Verfügung.
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
Die `SELECT` -Berechtigung für `sys.dm_os_host_info` erteilt der `public` standardmäßig zur Rolle. Gesperrt, erfordert `VIEW SERVER STATE` Berechtigung auf dem Server.   
 
>  [!CAUTION]
>  Ab Version [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.3, [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] erfordert die Version 17 `SELECT` -Berechtigung für `sys.dm_os_host_info` zum Herstellen von Verbindungen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Wenn `SELECT` Berechtigung aufgehoben `public`, nur Anmeldenamen mit `VIEW SERVER STATE` Berechtigung kann die neueste Version von SSMS eine Verbindung herstellen. (Andere tools, z. B. `sqlcmd.exe` verbinden, ohne `SELECT` -Berechtigung für `sys.dm_os_host_info`.)

  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt alle Spalten aus der **sys.dm_os_host_info** anzeigen.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Hier ist ein beispielresultset, das auf Windows festgelegt:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

Hier ist ein beispielresultset, die unter Linux festgelegt:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

