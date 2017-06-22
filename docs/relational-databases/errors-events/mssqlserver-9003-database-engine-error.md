---
title: MSSQLSERVER_9003 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 27d2fbf1bed8445eb8d3fd42000128741d2ee377
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
  
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
  

