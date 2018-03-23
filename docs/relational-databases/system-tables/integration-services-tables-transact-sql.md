---
title: Integration Services-Tabellen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
caps.latest.revision: ''
author: douglasl
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8c71350ec1e778b42fbeebf2a805fbb681f6e61
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services-Tabellen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In den Themen in diesem Abschnitt werden die Systemtabellen in der msdb-Datenbank beschrieben, in denen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendete Informationen gespeichert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 Enthält eine Zeile für jeden Protokolleintrag, der von einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket zur Laufzeit generiert wird.  
  
 Diese Tabelle wird nur verwendet, wenn Pakete den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Protokollanbieter verwenden.  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 Enthält eine Zeile für jeden logischen Ordner, den der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst zum Organisieren von Paketen verwendet. Spaltenwerte definieren die Über-/Unterordnungsbeziehungen zwischen geschachtelten Ordnern.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zeigt gespeicherte Pakete in einer hierarchischen Sicht an, wenn Sie eine Verbindung zu dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst herstellen.  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 Enthält eine Zeile für jedes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket.  
  
 Diese Tabelle wird nur verwendet, wenn Sie Pakete in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichern.  
  
  
