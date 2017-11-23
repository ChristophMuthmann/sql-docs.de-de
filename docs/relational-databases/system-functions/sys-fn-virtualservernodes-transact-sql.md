---
title: Sys. fn_virtualservernodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 404c45f4aa245d6aeba40ee11bdb6cf4ad98576e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnvirtualservernodes-transact-sql"></a>sys.fn_virtualservernodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Gibt eine Liste der Failoverclusterinstanz-Knoten zurück, auf denen eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden kann. Diese Informationen sind in Umgebungen mit Failoverclustering hilfreich.  
  
> [!IMPORTANT]  
>  Dies [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Systemfunktion wird aus Gründen der Abwärtskompatibilität. Wir empfehlen die Verwendung [dm_os_cluster_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md) stattdessen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
 Wenn der aktuelle Server auf einem Clusterserver ist **Fn_virtualservernodes** gibt eine Liste der Failoverclusterinstanz-Knoten auf dem diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiert wurde.  
  
 Wenn die aktuellen Serverinstanz kein gruppierter Server, ist **Fn_virtualservernodes** ein leeres Rowset zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss über die VIEW SERVER STATE-Berechtigung für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `fn_virtualservernodes` verwendet, um eine Abfrage auf einer Instanz eines gruppierten Servers auszuführen:  
  
```  
SELECT * FROM fn_virtualservernodes();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 NodeName  
  
 -------\-  
  
 SS3-CLUSN1  
  
 SS3-CLUSN2  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. dm_os_cluster_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Sys.fn_servershareddrives &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  
