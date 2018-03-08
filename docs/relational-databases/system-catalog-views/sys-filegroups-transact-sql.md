---
title: "\"Sys.FileGroups\" (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.filegroups_TSQL
- filegroups
- sys.filegroups
- filegroups_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.filegroups catalog view
ms.assetid: 9e851f72-1f8e-4515-a25d-152ebc12ed56
caps.latest.revision: "54"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91198ea3ed94496ff116014e0df2b1b067e4bf16
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysfilegroups-transact-sql"></a>sys.filegroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jeden Datenspeicher, der einer Dateigruppe entspricht.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<geerbte Spalten >**|--|Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [Sys. data_spaces &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**filegroup_guid**|**uniqueidentifier**|GUID für die Dateigruppe.<br /><br /> NULL = PRIMARY-Dateigruppe|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist der Wert NULL.|  
|**is_read_only**|**bit**|1 = Die Dateigruppe ist schreibgeschützt.<br /><br /> 0 = Auf die Dateigruppe besteht Lese-/Schreibzugriff.|  
|**"is_autogrow_all_files"**|**bit**|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> 1 =, wenn Sie eine Datei in der Dateigruppe erfüllt, die der Schwellenwert für automatische Vergrößerung, alle Dateien in der Dateigruppe vergrößert.<br /><br /> 0 =, wenn Sie eine Datei in der Dateigruppe erfüllt, die der Schwellenwert für automatische Vergrößerung, nur diese Datei vergrößert wird. Dies ist die Standardeinstellung.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Datenspeicher &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
