---
title: Sys. service_queue_usages (Transact-SQL) | Microsoft Docs
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
- sys.service_queue_usages
- sys.service_queue_usages_TSQL
- service_queue_usages
- service_queue_usages_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.service_queue_usages catalog view
ms.assetid: d58dcdaf-f82d-43d9-941b-f520581442bf
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da1ed1ec46b20074b00cf1c1b54ae1821353fd28
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysservicequeueusages-transact-sql"></a>sys.service_queue_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Katalogsicht gibt eine Zeile für jeden Verweis zwischen Dienst und Dienstwarteschlange zurück. Ein Dienst kann immer nur einer Warteschlange zugeordnet sein. Eine Warteschlange kann mehreren Diensten zugeordnet sein.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|Bezeichner des Diensts. Ist innerhalb der Datenbank eindeutig. Lässt keine NULL-Werte zu.|  
|**service_queue_id**|**int**|Bezeichner der Dienstwarteschlange, die von diesem Dienst verwendet wird. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sys.Services &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)  
  
  
