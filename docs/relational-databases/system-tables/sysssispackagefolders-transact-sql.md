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
ms.openlocfilehash: b4c3a4106a16be5c2f223ec253fcd9e5c8491daf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
