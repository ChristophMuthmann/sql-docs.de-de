---
title: sysdtspackagefolders (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
caps.latest.revision: 22
author: douglasl
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 179e6c1241ccbe42528eae591696727c9cea541a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden logischen Ordner in der Ordnerhierarchie, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet. Diese Ordner sind aufgeführt, in Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] für die Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. In einem Ordner sind Pakete aufgeführt, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder im Dateisystem gespeichert sind.  
  
 In der **parentfolderid** -Spalte wird die Ordnerhierarchie beschrieben. Der oberste Ordner in der Ordnerhierarchie enthält einen NULL-Wert in **parentfolderid**.  
  
 Die **foldername** -Spalte enthält den Namen der im Objekt-Explorer angezeigten Ordner.  
  
 Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|Der GUID des Ordners.|  
|**parentfolderid**|**uniqueidentifier**|Der GUID des Ordners, der als übergeordneter Ordner verwendet wird.|  
|**Ordnername**|**sysname**|Der Name des Ordners. Dieser Name wird in der Ordnerhierarchie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt.|  
  
  
