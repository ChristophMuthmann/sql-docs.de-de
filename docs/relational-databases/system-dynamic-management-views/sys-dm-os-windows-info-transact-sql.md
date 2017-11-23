---
title: dm_os_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 759ac050225bdc1abd78a6400152c6ee7f89dcfd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt in einer Zeile Informationen zur Windows-Betriebssystemversion zurück.  
  
  Gilt nur für SQL Server unter Windows ausgeführt wird. Verwenden Sie für SQL Server auf einem nicht-Windows-Host, z. B. Linux, auf ähnliche Informationen anzeigen [sys.dm_os_host_info &#40; Transact-SQL &#41; ](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|Für Windows gibt die Versionsnummer. Eine Liste der Werte mit Beschreibungen finden Sie unter [Betriebssystemversion (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx). Lässt keine NULL-Werte zu.|  
|**windows_service_pack_level**|**nvarchar(256)**| Für Windows gibt die Nummer des Service Packs an. Lässt keine NULL-Werte zu. |  
|**windows_sku**|**int**|Für Windows gibt die Windows Stock Keeping Unit (SKU)-ID. Eine Liste mit SKU-IDs und Beschreibungen finden Sie unter [Funktion "GetProductInfo"](http://msdn.microsoft.com/library/ms724358.aspx). Null zulässig ist. |  
|**os_language_version**|**int**| Für Windows gibt die Windows-Gebietsschemabezeichner (LCID) des Betriebssystems. Eine Liste mit LCID-Werten und Beschreibungen finden Sie unter [Von Microsoft zugewiesene Gebietsschemabezeichner (LCIDs)](http://go.microsoft.com/fwlink/?LinkId=208080). Lässt keine NULL-Werte zu.|  
  
  
## <a name="permissions"></a>Berechtigungen  
Die SELECT-Berechtigung für dm_os_sys_info wird standardmäßig die public-Rolle gewährt. Gesperrt, ist die VIEW SERVER STATE-Berechtigung auf dem Server erforderlich.  

## <a name="limitations-and-restrictions"></a>Einschränkungen
Verwenden Sie auf Hinweise SQL ausführen auf einem nicht-Windows-Host, z. B. Linux, finden Sie unter [sys.dm_os_host_info &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Spalten aus der Sicht **sys.dm_os_windows_info** zurückgegeben.  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 Hier ist ein Beispielresultset.  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

