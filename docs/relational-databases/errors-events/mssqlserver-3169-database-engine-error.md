---
title: MSSQLSERVER_3169 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 062f95d145ac25afe38db13561e7270d19db32cf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver3169"></a>MSSQLSERVER_3169
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3169|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|NA|  
|Meldungstext|Die Datenbank wurde auf einem Server der Version %ls gesichert. Diese Version ist mit diesem Server inkompatibel, da auf ihm die Version %ls ausgeführt wird. Stellen Sie die Datenbank auf einem Server wieder her, der die Sicherung unterstützt, oder verwenden Sie eine mit diesem Server kompatible Sicherung.|  
  
## <a name="explanation"></a>Erklärung  
Bestimmte funktionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wirken sich auf die Struktur der Datenbankdateien aus. Wenn Sie eine Datenbank auf einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wiederherstellen, ist das Dateiformat möglicherweise mit einer anderen Version von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nicht kompatibel.  
  
Dieser Fehler kann beispielsweise verursacht werden, wenn das Vardecimal-Speicherformat in einer höheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird und dann versucht wird, die Datenbankdateien in einer niedrigeren Version als [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 wiederherzustellen.  
  
## <a name="user-action"></a>Benutzeraktion  
Ermitteln Sie die Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf dem ursprünglichen Server ausgeführt wird. Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit der rechten Maustaste auf den Server und dann auf **Eigenschaften**, oder geben Sie in einem Abfragefenster **SELECT @@VERSION** ein. Öffnen Sie die Datenbank mithilfe der ursprünglichen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ermitteln Sie die funktionen, die für die ursprüngliche Datenbank in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert sind. Ändern Sie diese Einstellungen, um mit der Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu arbeiten, in der die Datenbank wiederhergestellt wird.  
  
