---
title: dm_io_cluster_shared_drives (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_shared_drives_TSQL
- sys.dm_io_cluster_shared_drives
- dm_io_cluster_shared_drives_TSQL
- dm_io_cluster_shared_drives
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_cluster_shared_drives dynamic management view
ms.assetid: c8fcced8-c780-49dc-99bd-6beb3ca532c4
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9c2b58ce7edec6128e1be77b6f22ac90c900a4a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmioclustershareddrives-transact-sql"></a>sys.dm_io_cluster_shared_drives (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  In dieser Sicht wird der Laufwerkname jedes freigegebenen Laufwerks zurückgegeben, wenn es sich bei der aktuellen Serverinstanz um einen gruppierten Server handelt. Wenn es sich bei der aktuellen Serverinstanz nicht um eine gruppierte Instanz handelt, wird ein leeres Rowset zurückgegeben.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_io_cluster_shared_drives**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**DriveName**|**nchar(2)**|Der Name des Laufwerks (der Laufwerkbuchstabe), das einen einzelnen Datenträger darstellt, der Teil des Arrays mit freigegebenen Clusterdatenträgern ist. NULL-Werte sind in der Spalte nicht zulässig.|  
|**pdw_node_id**|**int**|**Gilt für**: SsPDW<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Clusterunterstützung aktiviert ist, erfordert die Failoverclusterinstanz, dass die Daten- und Protokolldateien sich auf freigegebenen Datenträgern befinden, sodass möglicherweise auf sie zugegriffen werden kann, nachdem ein Failover zu einem anderen Knoten ausgeführt wird. Jede Zeile in dieser Sicht stellt einen einzelnen freigegebenen Datenträger dar, der von dieser gruppierten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird. Nur die in dieser Sicht aufgeführten Datenträger können zum Speichern von Daten- oder Protokolldateien für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden. Die in dieser Sicht aufgeführten Datenträger entsprechen denen, die sich in der der Instanz zugeordneten Clusterressourcengruppe befinden.  
  
> [!NOTE]  
>  Diese Sicht wird in einer zukünftigen Version als veraltet markiert. Wir empfehlen die Verwendung [dm_io_cluster_valid_path_names &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) stattdessen.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss über die VIEW SERVER STATE-Berechtigung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird sys.dm_io_cluster_shared_drives verwendet, um die freigegebenen Datenträger in einer Instanz eines gruppierten Servers zu bestimmen:  
  
```  
SELECT * FROM sys.dm_io_cluster_shared_drives;  
```  
  
 Dies ist das Ergebnis:  
  
 DriveName  
  
 --------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>Siehe auch  
 [dm_io_cluster_valid_path_names &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
