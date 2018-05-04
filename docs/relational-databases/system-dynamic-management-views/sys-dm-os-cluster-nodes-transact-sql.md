---
title: Sys. dm_os_cluster_nodes (Transact-SQL) | Microsoft Docs
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
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b612f3fed92d554ad6fcd9a5cf985eeea571de8c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosclusternodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt für jeden Knoten in der Konfiguration der Failoverclusterinstanz eine Zeile zurück. Wenn die aktuelle Instanz eine Failoverclusterinstanz ist, wird eine Liste mit Knoten zurückgegeben, in denen diese Failoverclusterinstanz (früher "virtueller Server") definiert ist. Wenn die aktuelle Serverinstanz keine Failoverclusterinstanz ist, wird ein leeres Rowset zurückgegeben.  
  
> **Hinweis:** von Aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_cluster_nodes**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**"Nodename"**|**sysname**|Name eines Knotens in der Failoverclusterinstanzkonfiguration (virtueller Server) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|status|**int**|Status des Knotens in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Failoverclusterinstanz: 0, 1, 2, 3, -1. Weitere Informationen finden Sie unter [GetClusterNodeState-Funktion](http://go.microsoft.com/fwlink/?LinkId=204794).|  
|status_description|**nvarchar(20)**|Beschreibung des Status des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterknotens.<br /><br /> 0 = aktiv<br /><br /> 1 = inaktiv<br /><br /> 2 = angehalten<br /><br /> 3 = verknüpfen<br /><br /> -1 = unbekannt|  
|is_current_owner|bit|1 bedeutet, dass dieser Knoten der aktuelle Besitzer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterressource ist.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Failoverclustering unterstützt wird, kann die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf jedem Knoten des Failoverclusters ausgeführt werden, der als Teil der Konfiguration der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz (virtueller Server) designiert ist.  
  
> **Hinweis:** diese Sicht ersetzt die Fn_virtualservernodes-Funktion, die in einer zukünftigen Version als veraltet markiert wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird sys. dm_os_cluster_nodes verwendet, um die Knoten in der Instanz eines gruppierten Servers zurückzugeben.  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|status|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|up|1|  
|node2|0|up|0|  
|Knoten3|1|down|0|  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_os_cluster_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [dm_io_cluster_shared_drives &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



