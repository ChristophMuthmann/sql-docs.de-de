---
title: MSSQLSERVER_9003 | Microsoft-Dokumentation
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
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 015fa28be4286d0444caa6ab66d9d7fb7326cdb3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9003|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LOG_INVALID_LSN|  
|Meldungstext|Die Protokollscannummer %S_LSN, die an den Protokollscan in der '%.*ls'-Datenbank übergeben wurde, ist ungültig. Dieser Fehler kann darauf hinweisen, dass Daten beschädigt sind oder dass die Protokolldatei (LDF) nicht mit der Datendatei (MDF) übereinstimmt. Falls dieser Fehler während der Replikation aufgetreten ist, müssen Sie die Veröffentlichung neu erstellen. Andernfalls stellen Sie die Datenbank von einer Sicherung wieder her, falls das Problem zu einem Fehler beim Starten führt.|  
  
## <a name="explanation"></a>Erklärung  
Eine Komponente hat eine ungültige Protokollfolgenummer an den Protokoll-Manager für die Datenbank übergeben. Die Ursache kann eine Replikation, eine Beschädigung oder eine mangelnde Übereinstimmung zwischen der primären Datendatei und dem Protokoll sein.  
  
## <a name="user-action"></a>Benutzeraktion  
Falls dieser Fehler während der Replikation aufgetreten ist, erstellen Sie die Veröffentlichung neu. Stellen Sie sie andernfalls aus einer Sicherungskopie wieder her.  
  
