---
title: dm_os_virtual_address_dump (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_virtual_address_dump
- sys.dm_os_virtual_address_dump_TSQL
- sys.dm_os_virtual_address_dump
- dm_os_virtual_address_dump_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_virtual_address_dump dynamic management view
ms.assetid: 7b24ea55-3873-42fd-a86c-441c92eb6175
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 451cc209f36a16341cb76ec6ae9319473480d541
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosvirtualaddressdump-transact-sql"></a>sys.dm_os_virtual_address_dump (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt Informationen zu einem Seitenbereich in einem virtuellen Adressraum des aufrufenden Prozesses zurück.  
  
> [!NOTE]  
>  Diese Informationen wird auch zurückgegeben, durch die **VirtualQuery** Windows-API.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_virtual_address_dump**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**region_base_address**|**varbinary(8)**|Zeiger auf die Basisadresse des Seitenbereichs. Lässt keine NULL-Werte zu.|  
|**region_allocation_base_address**|**varbinary(8)**|Zeiger auf die Basisadresse eines Seitenbereichs, der von der Windows-API-Funktion VirtualAlloc zugeordnet wird. Die Seite, auf die vom BaseAddress-Element gezeigt wird, ist in diesem Zuordnungsbereich enthalten. Lässt keine NULL-Werte zu.|  
|**region_allocation_protection**|**varbinary(8)**|Schutzattribute bei der ersten Zuordnung des Bereichs. Der Wert ist eine der folgenden:<br /><br /> -   PAGE_READONLY<br />-   PAGE_READWRITE<br />-PAGE_NOACCESS<br />-   PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-   PAGE_EXECUTE_READ<br />-   PAGE_EXECUTE_READWRITE<br />-   PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> Lässt keine NULL-Werte zu.|  
|**region_size_in_bytes**|**bigint**|Größe des Bereichs in Bytes (beginnend an der Basisadresse), in dem alle Seiten dieselben Attribute besitzen. Lässt keine NULL-Werte zu.|  
|**region_state**|**varbinary(8)**|Aktueller Status des Bereichs. Folgende Werte sind möglich:<br /><br /> -MEM_COMMIT<br />-MEM_RESERVE<br />-ADRESSRAUMS<br /><br /> Lässt keine NULL-Werte zu.|  
|**region_current_protection**|**varbinary(8)**|Die Schutzattribute. Der Wert ist eine der folgenden:<br /><br /> -   PAGE_READONLY<br />-   PAGE_READWRITE<br />-PAGE_NOACCESS<br />-   PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-   PAGE_EXECUTE_READ<br />-   PAGE_EXECUTE_READWRITE<br />-   PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> Lässt keine NULL-Werte zu.|  
|**region_type**|**varbinary(8)**|Identifiziert die Typen der Seiten in dem Bereich. Die folgenden Werte sind möglich:<br /><br /> -MEM_PRIVATE<br />-MEM_MAPPED<br />-MEM_IMAGE<br /><br /> Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


