---
title: MSSQLSERVER_9692 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e493fd5094abc25c1ff3c26edd3c6b6dc0ebc7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9692|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SB2_CANT_LISTEN_PORT_IN_USE|  
|Meldungstext|Der %S_MSG-Protokolltransport kann nicht an Port %d lauschen, weil er von einem anderen Prozess verwendet wird|  
  
## <a name="explanation"></a>Erklärung  
Ein anderes Programm auf dem Computer verwendet den angegebenen TCP-Port.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie **netstat -aon** aus, um zu bestimmen, welches Programm den Port verwendet. Deaktivieren Sie die entsprechende Anwendung, oder geben Sie einen anderen Port für Service Broker an.  
  
