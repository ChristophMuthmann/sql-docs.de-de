---
title: Sys. assembly_files (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.assembly_files
- assembly_files_TSQL
- assembly_files
- sys.assembly_files_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.assembly_files catalog view
ms.assetid: 1a384a2c-5556-4d12-a2ba-4da781363143
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcb6fd653e2fc9811d3153e7c547c0497560684f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysassemblyfiles-transact-sql"></a>sys.assembly_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Datei, aus der eine Assembly besteht.  
    
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|Die ID der Assembly, zu der die Datei gehört.|  
|**name**|**nvarchar(260)**|Der Name der Assemblydatei.|  
|**FILE_ID**|**int**|Die ID der Datei. Sie ist innerhalb einer Assembly eindeutig. Die Datei-ID 1 stellt die Assembly-DLL dar.|  
|**Inhalt**|**varbinary(max)**|Der Inhalt der Datei.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CLR-Assemblykatalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
