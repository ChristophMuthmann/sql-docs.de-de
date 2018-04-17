---
title: dbo.syscategories (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 99abe88da3eaa406096a4dffd7c7ff0176df5616
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält die Kategorien, die von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zur Organisation von Aufträgen, Warnungen und Operatoren verwendet werden. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID der Kategorie|  
|**category_class**|**int**|Elementart in der Kategorie:<br /><br /> **1** = Auftrag<br /><br /> **2** = Warnung<br /><br /> **3** =-Operator|  
|**category_type**|**tinyint**|Der Typ der Kategorie:<br /><br /> **1** = lokal<br /><br /> **2** = Multiserver<br /><br /> **3** = keine|  
|**name**|**sysname**|Name der Kategorie|  
  
  
