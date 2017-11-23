---
title: Sys.fn_servershareddrives (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_servershareddrives
- fn_servershareddrives_TSQL
dev_langs: TSQL
helpviewer_keywords:
- fn_servershareddrives function
- shared drives [SQL Server]
- names [SQL Server], shared drives
- sys.fn_serversharedrives function
ms.assetid: ff01eff7-8cb6-460c-ba7a-6a52bda6d471
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 519a95a83b8fd55dd306e3a2a3f0beb28e45aaf7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnservershareddrives-transact-sql"></a>sys.fn_servershareddrives (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Namen der freigegebenen Laufwerke zurück, die vom gruppierten Server verwendet werden.  
  
> [!IMPORTANT]  
>  Diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemfunktion wird aus Gründen der Abwärtskompatibilität bereitgestellt. Wir empfehlen die Verwendung [dm_io_cluster_valid_path_names &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_servershareddrives()  
```  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
 Wenn der aktuelle Server auf einem Clusterserver ist **Fn_servershareddrives** gibt den Namen des Laufwerks der freigegebenen Laufwerke zurück.  
  
 Wenn die aktuellen Serverinstanz kein gruppierter Server, ist **Fn_servershareddrives** ein leeres Rowset zurück.  
  
## <a name="remarks"></a>Hinweise  
 `fn_servershareddrives` gibt eine Liste der freigegebenen Laufwerke zurück, die von diesem gruppierten Server verwendet werden. Diese freigegebenen Laufwerke gehören zu derselben Clustergruppe wie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ressource. Außerdem ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressource von diesen Laufwerken abhängig.  
  
 Mit dieser Funktion lassen sich die Laufwerke ermitteln, die den Benutzern zur Verfügung stehen.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss über die VIEW SERVER STATE-Berechtigung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `fn_servershareddrives` verwendet, um eine Abfrage auf einer Instanz eines gruppierten Servers auszuführen:  
  
```  
SELECT * FROM fn_servershareddrives();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 DriveName  
  
 -------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>Siehe auch  
 [dm_io_cluster_valid_path_names &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [dm_io_cluster_shared_drives &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [Sys. fn_virtualservernodes &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)  
  
  
