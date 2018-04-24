---
title: MSSQLSERVER_1406 | Microsoft-Dokumentation
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
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0949d99e01e3b4f58060c1e1fbacc121e66639bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1406"></a>MSSQLSERVER_1406
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1406|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBM_BADSTATEFORFORCESERVICE|  
|Meldungstext|Der Dienst kann nicht auf sichere Weise erzwungen werden. Entfernen Sie die Datenbankspiegelung, und stellen Sie die "%.*ls"-Datenbank wieder her, um Zugriff zu erhalten.|  
  
## <a name="explanation"></a>Erklärung  
Der Dienst kann von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nicht erzwungen werden, da mit dem Spiegelungsstatus nicht garantiert werden kann, dass der erzwungene Dienstvorgang ordnungsgemäß funktioniert.  
  
## <a name="user-action"></a>Benutzeraktion  
Entfernen Sie die Datenbankspiegelung. Sie können anschließend die Spiegeldatenbank wiederherstellen, um Zugriff zu erhalten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erzwingen des Diensts in einer Datenbank-Spiegelungssitzung &#40;Transact-SQL&#41;](~/database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
[Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
